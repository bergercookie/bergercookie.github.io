---
author: bergercookie
categories:
- scratchpad
- programming
- linux
comments: true
date: "2020-03-10T20:00:00Z"
draft: false
title: Scratchpad - Linux Debugging Tools
toc: true
---

* [[rr]]
* [[gdbgui]] - Your de-facto debugging tool
    * Integrate gdbgui with rr - `gdbgui --rr`
* ldd, ldtree, ltrace, objump - [[display library dependencies]]
* [[strace|ltrace]], [[strace]]
* [[pmap]] - View the memory allocations for a particular process with *pmap*.
* [[valgrind]]
* [[gcc clang sanitizers]]
* [[Network debugging]]
* *dstat*
    Versatile tool for generating system resource statistics. Dstat is a
    versatile replacement for *vmstat*, *iostat* and *ifstat*
* [[perf|perf tools]]
* [[bcc tools|Collection of BCC tools]]
    * opensnoop - trace open() syscalls with file details. Uses Linux ftrace.
    * killsnoop - Track kill signals
* Cross-compilation debugger (?) : `aarch64-gnu-gdb`
