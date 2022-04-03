---
author: bergercookie
tags:
- Programming
- Linux
- Tooling
comments: true
date: "2021-05-01T00:00:00Z"
draft: false
title: 5 Albert Plugins to 5 Workflow Issues
showtoc: true
cover:
    image: "/images/albert-demos/example.png"
    alt: "Using Albert to boost your productivity"
    caption: "An image of the search plugins using `googler`"
    relative: false # To use relative path for cover image, used in hugo Page-bundles
---

This is part two of my articles on the Albert launcher. Read the first part
[here](/post/albert-plugins)

This post outlines 5 common issues that I had been facing during my day-to-day
development and the solutions that I came up with via 5 Albert plugins
respectively.

## TL;DR

The purpose of these plugins is a) to avoid context-switching and b) have a
single tool with a single interface instead X different tools with their own
corresponding interfaces.

All are hosted under the same github repo:
[awesome-albert-plugins](https://github.com/bergercookie/awesome-albert-plugins)
on github and here are links to each one of the plugins that I'll be discussing
below:

- [TLDR pages](https://github.com/bergercookie/awesome-albert-plugins/tree/master/plugins/tldr_pages)
- [Scratchpad](https://github.com/bergercookie/awesome-albert-plugins/tree/master/plugins/scratchpad)
- [Googler-enabled plugins](https://github.com/bergercookie/awesome-albert-plugins#plugins)
- [google_translate](https://github.com/bergercookie/awesome-albert-plugins/tree/master/plugins/google_translate) \| [words](https://github.com/bergercookie/awesome-albert-plugins/tree/master/plugins/words)
- [Saxophone](https://github.com/bergercookie/awesome-albert-plugins/tree/master/plugins/saxophone)

## 🔎 Looking up command / tool usage instructions

During your daily routine, you'll want to look up how to call a certain tool,
say recursively compress the contents of a directory using
[bzip](https://en.wikipedia.org/wiki/Bzip2), or create a new virtual environment
to work in using [Poetry](https://python-poetry.org/). You may either haven't
used these tools at all, or are not able to recall the exact flags for the task
at hand. Two common ways of dealing with this are:

- Google it! You'll then most probably want to move to a stackoverflow answer,
  copy-paste a command that seems to solve your issue, and then adjust it
  accordingly. This involves a few browser redirections (at least `google.com`
  -> `stackoverflow.com`), as well as the overhead of selecting the right post
  and finding the right answer to your question.
- Read the manpage / help page of the tool, if it has one. This resource may be
  more rigorous but it will also take more time to find the documentation section
  that you're interested in.

A more effective approach to this would be to use a software such as
[tldr](https://github.com/tldr-pages/tldr), [bro pages](http://bropages.org/),
or [cheat](https://github.com/cheat/cheat). More specifically, `tldr` allows
you to look up the most common usecases for a wide variety of tools, all without
leaving your command line. It's also easily extensible, allowing you to add more
examples to specific tools, or adding documentation and examples for new tools.

![tldr](/images/albert-demos2/tldr.svg)

However even in this case you have to switch context from what you're currently
doing; If you're working e.g., on VS Code, you have to start a new terminal,
look up the tool that you want, copy the usecase that you're interested in,
paste and modify it accordingly. We can do better than that.

Enter the [tldr_pages albert
plugin](https://github.com/bergercookie/awesome-albert-plugins/tree/master/plugins/tldr_pages)

![tldr-pages-albert](/images/albert-demos2/tldr-albert.gif)

It allows you to do fuzzy autocompletion-enabled search on any tldr command and
copy its content on ENTER. In addition you can also quickly navigate to the
appropriate webpage if you want to read more about the tool at hand, or fall
back to a google search if that's not good enough.

## 📓 Taking notes instantly - Refactor later

Whether I'm either reading articles on Wikipedia, watching videos on YouTube, or
doing pretty much anything on the computer that involves a bit of learning, I
like to take notes. A good approach to this would be to split your screen
vertically and have the browser on one side and your favorite editor on the
other. Then you would create a new text file for every new item you 're
studying, add a title, then add your notes or copy paste accordingly.

![scratchpad1](/images/albert-demos2/scratchpad1.png)

This involves a few steps in the process that can be improved:

- At that particular moment I don't want to have to:

  - create a new file
  - think of where to place it in my hierarchy of notes
  - add the appropriate title
  - add structure to the note that I'm taking

  I'd rather spend this time just recording my thoughts and reading through the
  actual Wikipedia page.

- I don't want to switch between reading the resource and recording my notes.

To deal with this, I'm using a very simple plugin called `scratchpad`.

![scratchpad2](/images/albert-demos2/scratchpad2.png)

Its logic is super simple. You write some text to it and it writes it to a file;
The same file all the time. You specify the path to that file the first time you
trigger the plugin.

![scratchpad3](/images/albert-demos2/scratchpad3.png)

Each text is saved there and by default it's formatted with a maximum width of
80 characters to assist in later potential reformatting. A blank line is
inserted between successive entries to the file and it allows to add a separator
if you start adding notes about a new subject

![scratchpad3](/images/albert-demos2/scratchpad3.png)

The plugin gets triggered either explicitly using `s<space>` or automatically
if your Albert query is longer than 5 words. This process allows you to record
anything you want and then sort them out later (i.e., place them into separate
files, structure them better, etc.).

![scratchpad4](/images/albert-demos2/scratchpad4.png)

Here's how your scratchpad looks like after a bunch of additions from two
different pages:

![scratchpad-final-result](/images/albert-demos2/scratchpad-final-result.png)

## 🔗 Adding Links during Text Editing

Another common issue is inserting links to other pages or documentation while
you're creating or editing an existing page. That may be a markdown document for
your GitHub repo, a Confluence page or Jira issue in your day job or a report
you're righting in LibreOffice. Most times you'd have to stop what you're doing,
launch your browser, search on google the thing you're interested in and
navigate to it, and finally, copy the link displayed in your browser prompt

Again, as with the previous issues discussed this approach takes too much time
_and_ makes you context switch from the thing you're currently doing.

Instead use [googler](https://github.com/jarun/googler) or even better one of
the many googler-enabled plugins in the
[awesome-albert-plugins](https://github.com/bergercookie/awesome-albert-plugins)
repo. You can basically use the
[create_googler_plugins.py](https://github.com/bergercookie/awesome-albert-plugins/blob/master/create_googler_plugins.py)
script after you've downloaded the repository to several Albert plugins, each
one responsible for searching in a single website. So for example, you can use
the trigger `gg` to search and get results for Google, or `gh` to search on
GitHub or `imdb` to search on IMDB.

Here's how it looks:

| ![](/images/albert-demos2/albert-suggestions-demo.gif) | ![](/images/albert-demos2/albert-suggestions-demo2.gif) |
| ![](/images/albert-demos2/albert-suggestions-demo3.gif) | ![](/images/albert-demos2/search_plugins.png) |

Using one of these plugins, for example the one that searches on Google, you can
search for and copy the link to the resource you're interested in without
leaving the document you're currently editing.

![](/images/albert-demos2/search-results.png)

## 🈯 Translating Text

Again, same premise as in the previous cases. You're reading an article or
watching a movie and you don't know a word or a phrase written there. It's too
much of a hassle to open a new browser tab, go to Google Translate to do the
translation.

Use the `google_translate` plugin in conjunction with the `word` plugin.

| ![](/images/albert-demos2/google_translate.png) | ![](/images/albert-demos2/word.png) |

The `google_translate` plugin will translate the word from the source language
to the destination language while you can also use the `auto` source to enable
autodetection.

The `word` plugin on the other hand will give you the definition of the given
word along with synonyms and antonyms.

## 🎷 Playing Radio Streams

This last plugin allows you to play and alternate between different stations
easily and without jumping around different webpages to do so.

It's called `saxophone`, and this is how its interface looks.

![](/images/albert-demos2/saxophone.png)

There's a bunch of preconfigured radios, specified in the
`config/saxophone.json` file. You can easily extend that list to include your
preferences as well.

Under the hood it uses the [VLC Remote-Control
Interface](https://wiki.videolan.org/documentation:modules/rc/).
