---
author: bergercookie
comments: true
date: "2020-07-04T10:34:21Z"
draft: false
title: Linux Code Commentary ... in a nutshell
toc: true
---

I recently got my hands on two books that talk about the Linux Kernel. These
are the [Linux Kernel in a
Nutshell](https://www.amazon.co.uk/Linux-Kernel-Nutshell-OReilly/dp/0596100795),
and [LINUX Core Kernel
Commentary](https://www.amazon.co.uk/Linux-Core-Kernel-Commentary-Knowledge/dp/1576104699).

![Linux Books](/images/linux-books.jpg)

These books are rather old, so some bits are outdated, but don't let this fact
discourage you. Both can be super useful and can definitely help you learn more
about how the Kernel works.

## Linux Kernel In a Nutshell

The first one is a classic. Written by [Greg
Kroah-Hartman](https://en.wikipedia.org/wiki/Greg_Kroah-Hartman), one of the
core Linux Kernel developers (who also took over as the lead of the project
[while Torvalds was
away](https://fortune.com/2018/09/17/linux-git-linus-torvalds-bullying-abuse-time-off/) ),
It doesn't require any prior knowledge of Linux (or even programming) and guides
the reader step by step into the process of building and configuring their
kernel from source. Some of its subjects include:

- How to get the Kernel sources.
- How to use `kconfig`.
- A short explanation into the most important `kconfig` flags as well as
  heuristics for when to enable each of them.
- Miscellaneous tools that help in building, maintaining and patching your
    kernel.

What's interesting about this book is that, it will give a short introduction
into each one of the technologies and hardware and the Linux kernel flags for
enabling/disabling support for them. Do you know what `SAMBA` or `SELinux` is?
Perhaps confused as to what the `lpj` or the `cachesize` CPU options are during
kernel configuration? This book will answer these questions.

This way you can learn about a bunch of components in just 20 pages (see
`Chapter 8: Configuration Recipes`) without having to jump to different webpages
and having to cross reference the validity of what's you're reading. Here are
some example topics:

- `PCI` Devices
  - `SATA`, `SCSI` and `IDE` Disk Controllers
  - `USB` Devices
  - Networking
- Filesystems
  - Types of supported filesystems (`FAT`, `CIFS`, `ZFS`)
  - `RAID`
- `CPU`s

## Linux Core Kernel Commentary

While the Linux Kernel in a nutshell is a rather lightweight read, this is
definitely not the case with the Linux Core Kernel Commentary. Counting 575 of
awkward landscape A4 pages it includes large chunks of code along with separate
pages with line-by-line explanation of the code.

What you will learn from it:

* How to read assembly code

  Even if you are unfamiliar going through assembly code, the book does a pretty
  good job at explaining how each one of the instructions work as well as offer
  alternative implementations of what's you are currently reading in `C` code.

* Understand concepts like *System Calls*, *Interrupts*, and *Virtual Memory*. On
  top of that it shows you the actual code used in the kernel that implements
  these. The latter can be so helpful. It shifts the reader's goal from "Let's have
  a theoretical discussion about X" to "Let's get down to the nitty-gritty
  details of how X is being done in a real-life production system".

* How Linux (well, at least its `2.3.12` version) actually works.

The content can be broken up into two parts. The first half contains the raw
contents of `C` and Assembly files from the kernel in a two-column format. The
second half contains the corresponding commentary for the selected files.

Based on these files, the book analyses the following subjects:

- Kernel Architecture Overview and Design Goals
- System Initializataion (What happens on system boot)
- System Calls (`system_call` and `lcall7`)
- Signals and Interrupts and Time
- Processes and Threads (Process Representation, Scheduling)
- Memory (Virtual Memory, Paging, Memory Mapping)
- IPC (Message Queues, Semaphores, Shared Memory)
- Symmetric Multiprocessing
- Tunable Kernel Parameters


Here's an example view of the code presented in the book (file:
`include/asm-i386/siginfo.h`).

![linux-code-view](/images/linux-code-view.png)

The black arrow on the right side indicates the page to go for a more in-depth
explanation.  Here are the contents of the explanation pages:

![linux-explanation-view](/images/linux-explanation-view.png)

It includes some introductory content about Interrupts and Signals and then it
goes line-by-line to explain what the purpose of the code is, what `struct`s it
uses etc.


## Conclusions

Get both of them and at least have them in your bookcase. They are pretty cheap
on <amazon.co.uk> and especially "Linux Kernel in a Nutshell" you can read
through it in a day or so (obviously allocate more time if you want to follow
along and explore the config parameters discussed). Regarding the "Core Kernel
Commentary" I don't expect to study it cover-to-cover, but it looks like a good
resource for picking a particular subject and learning as much as possible about
it.
