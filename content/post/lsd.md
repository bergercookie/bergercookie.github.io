---
author: bergercookie
tags:
  - Linux
  - Tooling
comments: true
date: "2020-03-10T20:00:00Z"
draft: false
title: Scratchpad - LSD - A colorful ls alternative
showtoc: true
cover:
    image: "/images/lsd-demo.png"
    alt: "Output of the LSD tool"
    caption: "Output of the LSD tool"
    relative: false
---

## Intro

[lsd](https://github.com/Peltoche/lsd) is an alternative to the classic `ls`
UNIX tool. It shows you a listing of files, directories, links, named pipes etc.
The difference to its predecessor is that it makes use of Glyph-rich fonts such
as [Nerd Fonts](https://github.com/ryanoasis/nerd-fonts) as well as an abundance
of colors preconfigured and available from start.

## Troubleshooting & How-to

### "Permission denied" when root or `$LD_PRELOAD` error on a `gtk3`-related library

You've probably installed lsd via `snap`. Don't; Either build it from source
or install it with `apt`.

### Use `lsd` and redirect its output

You might notice that when redirecting lsd output to e.g., a file, lsd
detects that its output is not actually a terminal and turns off coloring
and glyphs. Most of the time that's the correct behavior, otherwise it would
pollute the output file with escape characters for the colors. However if
you still want to keep colors and glyphs on, here's how you would do it

{{< highlight bash >}}
ls --tree --icon always --color always | less -r

# Or if piping to a file

ls --tree --icon always --color always | tee -a output-file
{{< / highlight >}}
