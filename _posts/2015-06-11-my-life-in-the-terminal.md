---
layout: post
title: My life in the terminal (WIP)
tags: development neovim shell
---

This is where I start to speak about my development enviroment, not sure if it
will be useful for someone, but for sure will help me when I start reinstalling everithing.
Most of the post will be about stuff in the terminal but at some points I cheat
and talk about some desktop applications that I find useful.
Grab some popcorn and enjoy.

---

<img src="http://i.imgur.com/hxeZDnh.jpg">

####Terminal
Just any modern terminal will suffice, just make sure it supports 256 colors. I
personally use Gnome terminal but that is because I found it has sane defaults
and easy to configure.

####Shell
I just love zsh, for me it's hard to explain why, maybe it is because it has o
lot of themes, maybe because it always suprises me when it autocompletes stuff
that I never tought it knew (git branches, tmux sessions, virtual enviroments)

Still on the shell, I use zpresto configuration, but fell free to try also
ohmyzsh as well.  Bonus stuff: vim bindings, super useful aliases for git,
tmux, etc.

####Tmux
This is the reason that I stick to developing in the terminal, provides tabs,
sessings, ability to switch betwenn tabs/projects with ease, spliting views,
views traversing. I realy recomend what crazy stuff people can come up with tmux
is regards to usage and configuration. Oh btw tmux is ridicuosly configurable.

####Tmuxinator
Neat little project. I use it to save my tmux project configurations so I can
jump right in projects. Tmuxinator makes tmux fun and confortable.

####Neovim
Another big player in my dev configuration. Neovim tries to take vim's code and
refactorit in order to make it more async, sane in order to attract more to
contributing to vim, and (my favorite) to make it embedable in other editors.
Just imagine the power of vim in a IDE like pycharm. If you like vim you will
love Neovim. Don't be fooled by the 'alpha' version, it's completly usable and
shows bugs verry rearly.

####Pudb
TUI python debugger, I love it because it offers everything you expect from a
modern debugger but at the same time lightweight and quick to invoke,
just insert: ``import pudb; pu.db`` and you are ready to go. Of course there
are dosens of ways you can start the thing but this is what I mostly use.
Bonus points: When selecting the default theme, it has that nostalgic Turbo
Pascal editor feel.

####PtPython/Bpython
Just because the python shell sucks. It has ipython under the hood, jedi for
autocomplection, multi-line code edit support, vim bindings *wink wink* and much
more. I you use python shell alot, scratch that, if you use the python shell
make yourself a favor and install ptpython. If we are still on the subject,
bpython is also cool, somethimes I switch between them because I don't know
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
everthing just works but this time faster. A must have tool for me.

####Happyfinder or 'hf' for the lazy ones
> hf is a command line utility to quickly find files and execute a command -
> something like Helm/Anything/CtrlP for the terminal. It tries to find the best
> match, like other fuzzy finders (Sublime, ido, Helm).

This is what README will tell you, I mostly use it for git add, quicly rm a file
or simply quick open it for editing. I see a lot of potential here but I always
fall back to old habits(shame shame).

####Tree
Tree is a recursive directory listing program that produces a depth indented
listing of files. I mostly use it to see a new project file structure or maybe I
want to show the file structure in a README, sound simple but comes verry handy
verry quicly.

####Vagrant
Create and configure lightweight, reproducible, and portable development
enviroments.
A pain in the ass, but that is because I never took the time to really
undestrant the configuration. The selling point is that you have all youre
project dependencies isolated, the bad thing is that it takes a lot of space and
if you manage several projects, size can get out of hand verry quicly, but at
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

####Gitg

TODO:

- terminal
terminal matters, term color pallete, terminal fonsts
- zsh
much cooler than bash, compatible with bash, awsome autocomplete sugestions,
with plugins completion/suggestions for git, tmux, doker, you name it
- zpresto
theme for zsh, much like omyzsh, tons of plugins, verry configurable
- tmux
this could not be possibile without tmux, tabs turbo charged
- tmuxinator
save tmux presets, an essential tool in my toolshed
- hf
fuzzy finder for files in folders, useful for quick opening a file for edit,
could be used with any command that takes a file as a paramater eg. git add, rm, cp, so on and so forth
- tree
super useful, displays directory strucure recursevly as a tree, can set the
depth of recursion
- ag
like grep but much much faster, super useful, I use it mostly in vim
- neovim
vim but with maitainable source code, active development, async functionality
builtin, lua plugins,
- pudb
debugger of choice, ncurse terminal debugger,
- ptpython
python shell on steroiz
- bpython
same as above, less features but more pleasent on the eye for me
- vagrant
- mosh
cool ssh client/server for laggy or unreliable internet connections
- gitg
this is where i cheat a bit, Gui git client, useful for big changes, big commits
- meld
THE BEST merge/diff tool out there for git, super useful
- midnight commander
For those who know total commander for windows will be quite at home with mc,
this time right in the terminal

next part I will talk about, configurations, vim plugins, and more.

