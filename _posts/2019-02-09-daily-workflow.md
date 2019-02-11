---
layout: post
title: "My daily workflow and tools"
date:   2019-02-09 15:28:00 +0000
categories: programming
author: bergercookie
published: true
permalink: /articles/dailly-workflow
comments: true
---

# WIP

As this is my first actual post I thought I'd write about something I'm a big
fun of, tooling. More specifically I want to describe my workflow when working
or in general when using my machine.

My general goal is to be productive in my day-to-day routine, and automate
everything that can actually be automated so that I can focus on the
higher-level tasks I'm interested in. I admit that sometimes I'm overdoing it
and automate a task that I don't actually have to but all in all I think this
attitude has helped me considerably so far.

I'm also a big believer in open-source; I'm striving to publish all my coding
projects on Github (see my [pinned repos](https://github.com/bergercookie) for
some of the works I'm proud of) and I've also been mentoring for the past two
years for the [Google Summer of Code
Project](https://summerofcode.withgoogle.com/) with the [MRPT robotics
organisation](https://mrpt.org). Thus, I'm trying as much as possible to use
open-source alternatives for all my tasks. That being said, if there is a
paid-for tool that does something great I'm happy to pay for it (e.g., see the
excellent `C/C++ Code Explorer` - [Sourcetrail](https://www.sourcetrail.com/)).

Here's a bullet list of the software I'm using:

- **OS:** GNU/Linux
- **Linux flavour:** Ubuntu/Debian
- **Desktop Environment:** [i3](https://i3wm.org/)
- **Editor:** [Vim/Neovim](https://github.com/neovim/neovim)
- **Browser:** Firefox
- **Terminal Emulator:** [Alacritty](https://github.com/jwilm/alacritty) + [Tmux multiplexer](https://github.com/tmux/tmux) + Bash

Let me now elaborate on the bullets above.

## GNU/Linux - Debian-flavours

Linux is free, as in freedom, it's ubiquitous and is simply the bestest
operating system there is; no reason to argue more on this point. Regarding
flavour, I simply use Debian or Ubuntu as the main operating system just because
I feel most comfortable in these systems It's nice know how to open all sorts of
files (`xdg-open`/`xdg-mime`) search for package names (`apt-cache`) install
packages / download sources (`apt-cache`, `apt-get`, `dpkg`) and in general know
how your system operates. Also being a roboticist by profession, there is a
strong inclination towards `Debian` / `Ubuntu` since
[ROS](https://ros.org)[^ros-ps] ships binaries for specifically for these
platforms and it's a total PITA to compile it from source. Finally I consider it
a big deal to always have a stable system even if that means not compiling your
project with the latest and greatest gcc-8 compiler. Ubuntu and Debian give you
that and also provide ways of installing more recent versions
([linuxbrew](http://linuxbrew.sh/), [Ubuntu
PPAs](https://launchpad.net/ubuntu/+ppas)) and hey, you can always compile stuff
from source if the previous don't work for you :wink:

[^ros-ps]: Don't know what ROS is? Google it or wait for me to write an article on its latest version `ROS2`.

## i3

TODO

## Vim/Neovim

There is a gazillion of articles on how to ... properly use vim or what to put
in your `vimrc` so I'm going to keep it short here.

Here are some of the plugins that I use on a daily basis and I'm confident have
boosted my editing efficiency significantly. Refer to the corresponding
`README`s for more details:

* Plugin manager: [vim-plug](https://github.com/junegunn/vim-plug)
* Asynchronous syntax checking/linting: [ale](https://github.com/w0rp/ale)
* Semantically-acurrate syntax highlighting: [chromatica](https://github.com/arakashic/chromatica.nvim)
* Indentation level detection: [detectindent](https://github.com/ciaranm/detectindent)
* Git client: [fugitive](https://github.com/tpope/vim-fugitive)
* `Printf`-like code debugging[^debugstring-ps]: [debugstring](https://github.com/bergercookie/vim-debugstring)
* UNIX helper functions: [eunuch](https://github.com/tpope/vim-fugitive)
* Asynchronous fuzzy searching: [fzf](https://github.com/junegunn/fzf.vim)
* Personal knowledge base /Task management: [vimwiki](https://github.com/vimwiki/vimwiki), [taskwiki](https://github.com/tbabej/taskwiki)


The important thing to note here is that you have to find a combination that
works for you.

* Don't use more plugins than you actually need or you'll bloat vim and you'll
    have awful startup times,
* Doublecheck that adding the plugin is worth the maintenance cost / potential
  startup overhead. Maybe already has a way of expressing it? Maybe it's just a
  matter of a single function in your `.vimrc`?

Finally, here's a link to my vim configuration in case you want to take a
better look: [vim-dotfiles](https://github.com/bergercookie/vim-dotfiles)


[^debugstring-ps]: Disclaimer: I am the author of vim-debugstring

## Firefox

Firefox is the de-facto open-source internet browser. It's fast, it's sleek and
using the new Firefox [WebExtensions](https://wiki.mozilla.org/WebExtensions)
and [tridactyl](https://github.com/tridactyl/tridactyl) one can browse the web
using `Vim` [^firefox-ps].

[^firefox-ps]: I know that Chrome also offers vim-like binding plugins but from my experience with them there's just a world of difference betweenthem and firefox plugins such as Tridactyl and its predecessors `Vimperator` / `Pentadactyl`.

## Alacritty/Tmux

`Alacritty` represents a newer trend in terminal emulators in that its objective
is to render the termnal output using the computer GPU. Other than that, its
developers strive to keep it minimal by **not** implementing additinal features
such as preferences window GUI (everything is managed by a `YAML` file) multiple
tabs, split panes etc and instead keep it simple and fast. For most of the
functionality that's omitted (e.g., split panes), they advice the usage of a
tool designed for that such as ... :drum: Tmux!

`Tmux` is the modern alternative to the good-old `screen` multiplexer. The big
difference compared to its predecessor is the good list of plugins and
customisation options it gives to its user. It comes with its own plugin manager
[tpm](https://github.com/tmux-plugins/tpm) along with plugins such as
[tmux-yank](https://github.com/tmux-plugins/tmux-yank),
[tmux-continuum](https://github.com/tmux-plugins/tmux-continuum)
, and [tmux-resurrect](https://github.com/tmux-plugins/tmux-resurrect) which
significantly enhance the Tmux user experience.

Finally, I'm using `Bash` for general navigation, system-interaction tasks. Bash
is the default Linux shell, and 99% of Linux machines you encounter will have
it. Yes, I am aware of `zsh` and the billion of plugins that it offers. In
general it is a superior shell compared to Bash but honestly the difference is
not big enough to counter for the fact that bash is ubiquitous and eventually
you'll be forced to used it when working on a new machine / someone else's
laptop.

## Miscellaneous UNIX-related tooling

This is a, rather long, list of tools that didn't fit any of the previous
categories but are still worth mentioning:

- **Password management:** [UNIX Password Pass](https://www.passwordstore.org/)

  I can't emphasise how easy and intuitive password management has been it
  since I came across `Pass`. It's a minimal tool built on top of well
  established software such as `GPG` (for encryption) and `Git` for version
  control. There is also a fully functional android app
  [PasswordStore](https://github.com/zeapo/Android-Password-Store) that syncs
  via git so you can have all your passwords in all your devices and actually
  reason on how the whole pipeline actually works.

- Fuzzy searching - autocompletion - directory navigation:



    Write about fzf, fzf-marks

- Rust-alternatives to classic UNIX tools




- **E-Book/Scientific works management:** [Calibre](https://calibre-ebook.com/)

    Calibre is an open-source e-book management tool written in Python. Apart
    from its obvious task, it can sync your books with Kindle or android devices
    it can import and manage various formats (e.g., `pdf`, `mobi`), and it can
    also has a pretty decent android client.


## More on the menu


As this is my first post, feel free to add some feedback in the comments and let
me know what you think of this.

In the 
