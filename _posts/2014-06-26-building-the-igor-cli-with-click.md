---
layout: post
title: Building the Igor CLI with Click 
tags: gsoc2014
---

This summer, I am building an [IPMI][3] [management console][2] for the [OSUOSL][1]. IPMI
is the interface implemented by special hardware that lets you command a machine over a network
as long as it is plugged in, even if the machine is powered off or refuses to
boot an OS. If you have ever had ops engineers rebooting a bricked datacenter server with a magic
console, you have seen IPMI.

There are some requirements to working with IPMI: you need to have commands such as `ipmitool`
available on your OS, and you need to know the IPMI credentials for the machine you want to access.
If your datacenter machine has many IPMI users, or if they would like access via smartphones and web
browsers, you quickly hit some limitations. Sharing the single IPMI username and
password for the machine with all your users is a bad idea. Additionally, `ipmitool`
equivalents for mobile OS's are few and brittle.

I planned to address this with the following scheme: implement a REST API
that calls `ipmitool` commands, and then have very thin CLI, web GUI and Android clients that 
consume this REST API. These thin clients interface with the REST API to manage users, machines and
user-machine permissions in addition to actually performing the IPMI operations.

Here I discuss the CLI design and implementation with a recent Python CLI framework called
[Click][4], by [Armin Ronacher][5] of [Flask][6], [Werkzeug][7] and [itsdangerous][8] fame.
While it may seem like a natural choice once you are done reading this post, note that I had
to throw away a bunch of code after a false start with a different but way more popular
CLI framework. Before I get into that, let us look at some of the goals I had for the CLI.

## Hierarchical Commands

If you have used the `heroku` CLI, you already know what this means. Since a [termshow][9] is
worth a thousand man-pages, here is one below:

<div class="frame">
  <iframe src="http://showterm.io/b39f439e874d0eae8e9ee" scrolling="no" frameborder="0"></iframe>
</div>

The workflow above shows a new Igor user who wants to view the available machines. She knows
nothing about Igor, and begins by typing in the command itself. She then navigates to the `machines`
command and finds the `list` subcommand, and is then directed towards authorizing herself with the
`auth` command and finally viewing the list of machines.

This demonstrates some important features that I wanted Igor to have. 

**Explorability.** Nobody likes reading a monochrome wall of text that is the typical manpage.
A sensible, simple hierarchy with up-to-date documentation and helpful error messages is
enough for the average user to navigate the average CLI, just like how you would explore a new website.
An added bonus would be friendly and forgiving prompts for when the user forgets to provide
any required options.

**Extensibility.** APIs change constantly. Updating your CLI to match a new API endpoint
should not require touching too many files. Ideally, you would just add a single new Python module
for a new command that also contains all its subcommands, and have everything else in the hierarchy
fall into place.

**DRYness.** Subcommands may share the need for certain data that could be handled by
their common parent instead of in each of them individually. A common case is having a
`--verbose` option: instead of being parsed by every subcommand, have the root command parse
and store this in a configuration object that is available to all subcommands.

An additional aesthetic requirement is that the CLI mirror the hierarchical structure of the REST API,
so users of both can switch contexts easily.

How would one go about quickly implementing such a design? A probable first step would be
looking at the [Python Guide][10] for recommendations and figuring out what the most popular
CLI framework out there is.

## A False Start

If you started this way, you would come across and immediately fall for the incredibly sexy [docopt][11].
To see why, here is an example of parsing CLI options with docopt:

{% highlight python %}
"""Naval Fate.

Usage:
  naval_fate.py ship new <name>...
  naval_fate.py ship <name> move <x> <y> [--speed=<kn>]
  naval_fate.py ship shoot <x> <y>
  naval_fate.py mine (set|remove) <x> <y> [--moored|--drifting]
  naval_fate.py -h | --help
  naval_fate.py --version

Options:
  -h --help     Show this screen.
  --version     Show version.
  --speed=<kn>  Speed in knots [default: 10].
  --moored      Moored (anchored) mine.
  --drifting    Drifting mine.

"""
from docopt import docopt


if __name__ == '__main__':
    arguments = docopt(__doc__, version='Naval Fate 2.0')
    print(arguments) 
{% endhighlight %}

docopt constructs argument parsing rules from your docstring. Hence,
you end up with well-written, up-to-date documentation for your commands,
and your code remains minimal. To complete things, docopt comes with many
[examples][12], including one partially implementing the complex [git][13]
CLI.

However, you simply cannot implement the hierarchy I described above without
a lot of additional effort. I personally think the provided git example is
a joke: `git help <command>`, the first hierarchical composition of commands
I wanted to try, [does not work][14]. I spent some time on this and concluded
that it is non-trivial to try and get it to work either.

I hated throwing away this tiny method dressed in a beautiful docstring that takes care
of everything for you. But sometimes things just don't work out.

Click satisfied the aforementioned goals perfectly. It is a solid, well-designed
library that is similar to Flask in its excellent documentation, and abundance of Python
decorators. In short, it had what I needed:

   1. Arbitrarily nested commands with minimal code.
   2. Automatic help-page generation.
   3. Prompts for required but unprovided options.
   4. Sharing data between commands via a shared object.

Let us look at some of the more interesting internals of the Igor CLI implementation.

## Authentication

The Igor REST API uses token-based authentication: you first request an API token by providing
your username and password, and all subsequent requests must contain this API token. The API
token has an expiry date and is generally a better idea than sending your username and password
with every API request.

For credential management, the Igor CLI again follows the lead of `heroku`.
Once a user successfully logs in using `igor auth login`,
the username and API token are stored in `~/.netrc`, which is a
standard flat-file used for credential storage. It looks like this:

{% highlight ApacheConf %}
machine code.heroku.com
  login username@domain.com
  password asd0as9d0a9s0d90as9d0a9s0d90as9d09as0d9
machine api.heroku.com
  login username@domain.com
  password asd0as9d0a9s0d90as9d0a9s0d90as9d09as0d9
{% endhighlight %}

The [netrc][15] Python module helps you read the `~/.netrc` file into a Python dictionary, but
unlike the eponymous Ruby [gem][16], it does not provide a way to save dictionaries back to
well-formatted `~/.netrc` files. I had to write some [helper methods][17] to do this.

Why store credentials in this file? Being a pretty standard storage
location, many other tools use this as the default source of credentials, like FTP and,
importantly for us, the Python [requests][18] module that eases working with HTTP in Python.
It automatically picks up credentials from `~/.netrc` and provides
them to the correct host. Hence, by having these credentials stored in `~/.netrc`,
we could avoid additional code anywhere else that retrieves and sends them across with
HTTP requests.

A natural question now would be: what about validation? What if the requests module does not
find any stored credentials? What happens if the user does something strange; for
example, setting a machine's power state to `monkey` instead of the valid `on|off|reset|cycle`
options?

## Handling Errors

The Igor CLI is a thin layer over the Igor REST API, which is a thin layer over `ipmitool`. This
appears really fragile; if each layer performs its own argument parsing and validation, doing
something like adding new argument parameters would require changing each layer.

The strategy I adopted is to aggressively delegate error handling, and enforce some invariants.
The Igor CLI uses a single `make_api_request` method defined [here][19]. If the user is not logged
in or is not authorized to access a machine, the function fails with a pointer to `igor auth` or
`igor permissions`. For any other API response apart from HTTP 200 OK, the method bails out
immediately, printing the API response. So the CLI subcommands themselves are simply messengers,
performing no validation themselves.

As an example, consider the `ipmitool power` command that takes exactly one of `on|off|reset|cycle`
as a `state` parameter. The Igor CLI takes the `--state` argument and sends it to the Igor
REST API. The REST API in turn passes it on to `ipmitool` via the [pyipmi][20] module, which raises
an `IpmiError` if there is anything wrong. If such an exception occurs, the API returns
a message (with a HTTP 400 error), which is then displayed by the CLI's `make_api_request` function.

With this strategy, if `ipmitool` begins accepting a new `monkey` power state, we would not need any
code changes at all!

## Future

The Igor CLI is easily installable using [pip](https://pypi.python.org/pypi/pip):

{% highlight bash %}
pip install git+https://github.com/emaadmanzoor/igor-cli.git
{% endhighlight %}

It currently allows one to add, remove, view and update users, machines and user-machine
permission pairs. It also allows one to view and set a machine's power state. The remaining IPMI
operations are work in progress. A particularly interesting one is interacting with the serial-on-LAN
console; would it make sense to create some sort of persistent duplex HTTP connection? Also coming
up are the ncurses, web and Android clients. Further details are available in
my [project proposal and timeline][21].

There will soon be a post describing the Igor REST API too. You can stay updated with new
developments by watching or starring the [Igor CLI][22] and [Igor REST API][23] projects on Github.

## Appendix

This appendix provides termshows demonstrating some of the less interesting command groups that
were not discussed in the post above. All commands were executed as Igor user `root`.

The Igor REST API server was running locally. Instead of passing the `--igor-server`
option with every command, the following is placed in `~/.igorrc`:

{% highlight ApacheConf %}
[igor]
igor_server = localhost:5000
{% endhighlight %}

### Authentication Operations

*See [pull request](https://github.com/emaadmanzoor/igor-cli/pull/2).*

<div class="frame">
  <iframe src="http://showterm.io/a6c94469d81690371b084" scrolling="no" frameborder="0"></iframe>
</div>

### Machine Management Operations

*See [pull request](https://github.com/emaadmanzoor/igor-cli/pull/3).*

<div class="frame">
  <iframe src="http://showterm.io/44b89c6eab991b6f24dc3" scrolling="no" frameborder="0"></iframe>
</div>

### User Management Operations

*See [pull request](https://github.com/emaadmanzoor/igor-cli/pull/4).*

<div class="frame">
  <iframe src="http://showterm.io/c15a606f80486ae4af2a0" scrolling="no" frameborder="0"></iframe>
</div>

### Permission Management & Power State Operations

Permission management: *See [pull request](https://github.com/emaadmanzoor/igor-cli/pull/5).*

IPMI power state: *See [pull request](https://github.com/emaadmanzoor/igor-cli/pull/6).*

<div class="frame">
  <iframe src="http://showterm.io/7b469f028bbe3821467af" scrolling="no" frameborder="0"></iframe>
</div>

[1]: http://osuosl.org/
[2]: https://www.google-melange.com/gsoc/project/details/google/gsoc2014/emaadmanzoor/5693417237512192
[3]: http://en.wikipedia.org/wiki/Intelligent_Platform_Management_Interface
[4]: http://click.pocoo.org/
[5]: http://lucumr.pocoo.org/
[6]: http://flask.pocoo.org/
[7]: http://werkzeug.pocoo.org/
[8]: http://pythonhosted.org/itsdangerous/
[9]: http://showterm.io/
[10]: http://docs.python-guide.org/en/latest/scenarios/cli/
[11]: http://docopt.org/
[12]: https://github.com/docopt/docopt/tree/master/examples
[13]: https://github.com/docopt/docopt/tree/master/examples/git
[14]: https://github.com/docopt/docopt/issues/196
[15]: https://docs.python.org/2/library/netrc.html
[16]: https://rubygems.org/gems/netrc
[17]: https://github.com/emaadmanzoor/igor-cli/blob/master/cli/netrc_utils.py
[18]: https://python-requests.org
[19]: https://github.com/emaadmanzoor/igor-cli/blob/master/cli/request_utils.py
[20]: https://pypi.python.org/pypi/pyipmi
[21]: http://www.google-melange.com/gsoc/proposal/public/google/gsoc2014/emaadmanzoor/5724160613416960
[22]: https://github.com/emaadmanzoor/igor-cli
[23]: https://github.com/emaadmanzoor/igor-rest-api
