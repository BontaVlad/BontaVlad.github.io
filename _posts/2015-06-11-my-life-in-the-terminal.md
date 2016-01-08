---
layout: post
title: My life in the terminal (WIP)
tags: development neovim shell narcissism
---

This is where I start to speak about my development environment, not sure if it
will be useful for someone, but for sure will help me when I start reinstalling everything.
Most of the post will be about stuff in the terminal but at some point I cheat
and talk about some desktop applications that I find useful.
Developing in the terminal is not everyones cup of tea, but even if you are a
IDE wizard maybe you can find something that could help you make things
faster, more pleasant to work with.

---

<img src="http://i.imgur.com/hxeZDnh.jpg">

This is my high-level development configuration, stuff that I use getting shit
done on a daily basis, for sure I forgot some.

####OS
Mostly I worked with the Debian family, but more and more ArchLinux throws me
seductive stares. Current setup involves Elementary OS with Numix theme(looks
quite good) but lately I have some performance problems and I said "Fuck it, I
will install Archlinux with Awesome window manager".

####Terminal
Just any modern terminal will suffice, just make sure it supports 256 colors. I
personally use Gnome terminal but that is because I found it has sane defaults
and easy to configure.

####Shell
I just love zsh, for me it's hard to explain why, maybe it is because it has a
lot of themes, maybe because it always surprises me when it alto completes stuff
that I never thought it knew (git branches, tmux sessions, virtual environments)

Still on the shell, I use prezto configuration, but fell free to try also
oh-my-zsh as well.  Bonus stuff: vim bindings, super useful aliases for git,
tmux, etc.

####Tmux
This is the reason that I stick to developing in the terminal, provides tabs,
sessions, ability to switch between tabs/projects with ease, splitting views,
views traversing. I really recommend going on youtube and watching what crazy stuff
people can come up with tmux is regards to usage and configuration.
Oh by the way tmux is ridiculously configurable.

####Tmuxinator
Neat little project. I use it to save my tmux project configurations so I can
jump right in projects ``mux start the_project``.
Tmuxinator makes tmux fun and comfortable.

####Neovim
Another big player in my dev configuration. It's vim but with maintainable
source code, active development, async functionality built-in, lua plugins,
and (my favorite) embeddable in other editors(not there yet), just imagine the power of vim in a
IDE like Pycharm. If you like vim you will love Neovim.
Don't be fooled by the 'alpha' version, it's completely usable and bugs only show
up rarely.

####VirtualEnv Wrapper
If you develop in python you know what VirtualEnv wrapper does if not than you
don't need it.

####Pudb
TUI python debugger, I love it because it offers everything you expect from a
modern debugger but at the same time lighweight and quick to invoke,
just insert: ``import pudb; pu.db`` and you are ready to go. Of course there
are dozens of ways you can start the thing but this is what I mostly use.
Bonus points: When selecting the default theme, it has that nostalgic Turbo
Pascal editor feel.

####PtPython/Bpython
Just because the python shell sucks. It has ipython under the hood, jedi for
auto completion, multi-line code edit support, vim bindings *wink wink* and much
more. I you use python shell allot, scratch that, if you use the python shell
make yourself a favor and install ptpython. If we are still on the subject,
bpython is also cool, sometimes I switch between them because I don't know
which one I like more.

####Midnight Commander
If you ever used Total Commander on windows then this TUI application is for
you. I like to do as much as I can in the terminal so when I have some
complicated stuff dealing with files I fire this baby up and get right to it,
works like a breeze and if you are still uninterested let me finish with this:
**It has vim bindings (you must enable them)**

####The Silver Searcher or 'ag' for short
A code searching tools similar to ``ack`` or ``grep`` but much much faster.
What can I say more, if something uses ``ack`` or ``grep`` just make a alias and
everything just works but this time faster. A must have tool for me.

####Happyfinder or 'hf' for the lazy ones
> hf is a command line utility to quickly find files and execute a command -
> something like Helm/Anything/CtrlP for the terminal. It tries to find the best
> match, like other fuzzy finders (Sublime, ido, Helm).

####feh
feh is an X11 image viewer aimed mostly at console users.
Unlike most other viewers, it does not have a fancy GUI, but simply displays
images. It is controlled via command line arguments and configurable key/mouse actions.
Quick and dirty way to check out some images without leaving the comfort of the
terminal.

This is what README will tell you, I mostly use it for git add, quickly rm a file
or simply quick open it for editing. I see a lot of potential here but I always
fall back to old habits(shame shame).

####Tree
Tree is a recursive directory listing program that produces a depth indented
listing of files. I mostly use it to see a new project file structure or maybe I
want to show the file structure in a README, sound simple but comes very handy
very quickly.

####Vagrant
Create and configure lightweight, reproducible, and portable development
environments.
A pain in the ass, but that is because I never took the time to really
understand the configuration. The selling point is that you have all your
project dependencies isolated, the bad thing is that it takes a lot of space and
if you manage several projects, size can get out of hand very quickly, but at
the same time if you want to work on a project ``vagrant up`` and you are
golden.

####Mosh
Remote terminal application that allows roaming, supports intermittent
connectivity, and provides intelligent local echo and line editing of user keystrokes.

Mosh is a replacement for SSH. It's more robust and responsive,
especially over Wi-Fi, cellular, and long-distance links.

I use mosh on low quality connections, either huge lag or connections that keep
dropping, the bad part is that it requires mosh to be installed also on the
server and that is not always possible(most of the time). Works great when it
works but I have fewer chances to use it.

####Meld
Meld is a visual diff and merge tool targeted at developers.
Meld helps you compare files, directories, and version controlled projects.
Like I said before I am a terminal fanatic, but when it comes to merge
conflicts, diff between files, I much rather do it in meld. In my case it's the
best tool for the job, not to mention that it's free.

####Gitg
gitg is the GNOME GUI client to view git repositories.
Again, when dealing with git I like to GUI stuff up. Everybody has some guilty
pleasures, feels kinda nice to cheat on my terminal, make me like him more.

Bare with me for part II where I will talk about configurations, vim plugins,
and more.
