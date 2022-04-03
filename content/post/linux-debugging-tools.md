---
author: bergercookie
tags:
  - Linux
  - Tooling
categories:
  - Scratchpad
comments: true
date: "2020-03-10T20:00:00Z"
draft: true
title: 🛠️ Scratchpad - Linux Debugging Tools
showtoc: false
cover:
  image: "/images/linux-dbg.png"
  alt: ""
  caption: "Linux Debugging Tools"
  relative: false
---

- [[rr]]
- [[gdbgui]] - Your de-facto debugging tool
  - Integrate gdbgui with rr - `gdbgui --rr`
- ldd, ldtree, ltrace, objump - [[display library dependencies]]
- [[strace|ltrace]], [[strace]]
- [[pmap]] - View the memory allocations for a particular process with _pmap_.
- [[valgrind]]
- [[gcc clang sanitizers]]
- [[Network debugging]]
- _dstat_
  Versatile tool for generating system resource statistics. Dstat is a
  versatile replacement for _vmstat_, _iostat_ and _ifstat_
- [[perf|perf tools]]
- [[bcc tools|Collection of BCC tools]]
  - `opensnoop` - trace open() syscalls with file details. Uses Linux ftrace.
  - `killsnoop` - Track kill signals
- Cross-compilation debugger: Use `aarch64-gnu-gdb`
