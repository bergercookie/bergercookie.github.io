---
author: bergercookie
categories:
- programming
- linux
comments: true
date: "2020-03-08T20:00:00Z"
draft: false
tags: scratchpad
title: Scratchpad - Linux Tooling
---

A scratchpad of techniques, tools, and routines that I tend to use on my Linux
machines. Most probably not all of these bullets are going to be useful in your
case, but I hope that at there will be at least a 10% of them which you won't
have come across before or that you'll find useful and add to your arsenal.

P.S. Parts wrapped in `[[  ]]` are links to articles not added yet.

### HTOP - Do not show individual user threads / group them all under the process

Just press `H`. This is handy for monitoring the memory/CPU usage of the whole
process instead of just its threads.

### Set the time / timezone

{{< highlight bash >}}
sudo dpkg-reconfigure tzdata
# OR
cp /usr/share/zoneinfo/America/La_Paz /etc/localtime
{{< / highlight >}}

### Permission denied on chown even as root

{{< highlight bash >}}
lsattr <filename>
chattr -i <filename> # "i"-immutable file attribute
{{< / highlight >}}

### Monitor the progress of dd

There are multiple alternatives to solve this. Newer versions of dd support
`status=progress`. If you're on an older version, use one of the following:

* pv - put in in between `if=...` and after `of=...`

{{< highlight bash >}}
dd if=image_rpi_20180712.img bs=1M | pv | sudo dd of=/dev/mmcblk0
{{< / highlight >}}

* Use [Xfennect/progress](https://github.com/Xfennec/progress)

### Redirect-dmesg-to-console

Imagine cases that the whole UI has frozen or , for some unknown reason, the
OS has lost connection to the storage and you cannot read/write to disk. In such
cases you cannot `cat /var/log/syslog` since that would require reading from
disk. Having kernel logs automatically redirected to a virtual console offers a
solution to these problems

Add the following line to `/etc/syslog.conf` /  `/etc/rsyslog.conf`

{{< highlight syslog >}}
kern.* /dev/tty10
{{< / highlight >}}

Alternatively if you don't want to modify preexisting system configuration
files, you can add your rules to a new file under `/etc/rsyslog.d/`.

In addition to this, I also want to periodically write dmesg output to a file.
To do that I have the following rule in the crontab of `root`:

{{< highlight bash >}}
*/60  * * * *  dmesg -Tx > /home/berger/$(date +\%Y\%m\%d)_dmesg_output.dmesg
{{< / highlight >}}

This will write dmesg output to a file, prefixed with the current date
e.g., `20200229_dmesg_output.dmesg`, under my home directory every 1 hour

In the previous line I'm using the `-T` and `-x` flags of `dmesg`:

* `-T` -> Show the time
* `-x` -> Decode logging level

Source: <https://superuser.com/a/30133/369517>

### Sort letters in a case-sensitive way

It seems that the default `sort` utility shipped with ubuntu sorts by default in
a case insensitive way. This leads to 'a' coming ahead of 'C' even though the
latter has a lower value in the [ASCII table](http://www.asciitable.com/).

To correct this you have to override the `*_COLLATE` environment variable:


{{< highlight bash >}}
echo -e "c\nb\nB\na" | LC_COLLATE=C sort
# or with UTF-8 encoding
echo -e "c\nb\nB\na" | LC_COLLATE=C.UTF-8 sort
{{< / highlight >}}

## Articles to read

* The Art of the Command Line: <https://github.com/jlevy/the-art-of-command-line>
* Linux security tools and practices:
    * <https://blog.quarkslab.com/clang-hardening-cheat-sheet.html>
    * <https://wiki.debian.org/Hardening>
    * <https://github.com/yellowbyte/reverse-engineering-reference-manual/blob/master/contents/anti-analysis/Anti-Debugging.md>
* Electronics design: http://www.kicad-pcb.org/

## Useful Tools

### UNIX Classics

* tee: Redirect both `stderr` and `stdout` to file: `./a.out |& tee output`
* [ufw](https://help.ubuntu.com/community/UFW): The Uncomplicated Firewall - Frontend to `iptables`
    * [Introduction](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-14-04)
    * [Cheatsheet](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands)

#### [Moreutils](http://joeyh.name/code/moreutils/)

`chronic`: runs a command quietly unless it fails
`combine`: combine the lines in two files using boolean operations
`errno`: look up errno names and descriptions
`ifdata`: get network interface info without parsing ifconfig output
`ifne`: run a program if the standard input is not empty
`isutf8`: check if a file or standard input is utf-8
`lckdo`: execute a program with a lock held -> Use `flock` instead!
`mispipe`: pipe two commands, returning the exit status of the first
`parallel`: run multiple jobs at once
`pee`: tee standard input to pipes
`sponge`: soak up standard input and write to a file
`ts`: timestamp standard input

{{< highlight bash >}}
ls | ts "%.S" # subsecond accuracy
{% endhighlight bash%}

`vidir`: edit a directory in your text editor
`vipe`: insert a text editor into a pipe
`zrun`: automatically uncompress arguments to command


### Miscellaneous tools

* safe-rm - Ubuntu package
* [GrapheneX hardening tool](https://pypi.org/project/graphenexr)

### Hidden Gems

* Google Search from command line: <https://github.com/jarun/googler>
* fzf - fuzzy finding CTRL_T, CTRL_R, ALT_C
* pee from moreutils - "tee standard input to pipes"
* Remove color codes from command outptu

  * `./somescript | sed -r "s/\x1B\[([0-9]{1,2}(;[0-9]{1,2})?)?[mGK]//g"`

* rtv - Terminal client for reddit
* units - GNU currency/units conversion script
* pv - Pipe Viewer
    * <http://www.catonmat.net/blog/unix-utilities-pipe-viewer/>
    * How fast do we read from `/dev/zero`?
        * `pv /dev/zero > /dev/null`
    * Transfer a file and see the progress of it (A -> B)
        * `tar -cf - /path/to/dir | pv | nc -l -p 6666 -q 5` (A)
        * `nc 192.168.1.100 6666 | pv | tar -xf -` (B)
    * Compress contents of a directory
        * `tar -cf - . | pv -s $(du -sb . | awk '{print $1}') | gzip > out.tgz # WITH TIME`
        * `tar -czf - . | pv > out.tgz WO END TIME`
* Options for effective, git-aware `tar`ring:

{{< highlight bash >}}
tar cvfz <git-repo>.tgz --exclude-vcs --exclude-vcs-ignores <...>/.gitignore --exclude='<git-repo>/.gitmodules'  <git-repo>
tar cvfz <name>.tgz --exclude-vcs --exclude-vcs-ignores ~/<name>/.gitignore --exclude='~/<name>/.gitmodules' -C ~/<name>/src/
tac -rs # Concatenate and print files in reverse
{{< / highlight >}}

* Rg
    * Standard search in directory
      * `rg find_package /usr/share/`
    * search in specific filetypes -> h, hpp, cpp
        * `rg <string-to-search> <path> --type-add "source:*.{h,hpp,cpp}" -tsource`
* [[sed]]
* [[awk]]
* [[sftp]]
* `goldendict` - gd -> plays well with albert
    * CTRL-C-C to translate word from keyboard
* [[telnet]]
* [[openssl]]
* netstat/fuser:
    * Find what process is using port 80
        `netstat -tulpn | grep 80`
        `fuser 80/tcp`
* nc - arbitrary TCP/UDP connections and listen
    * for server: nc -l localhost 30000
      for client: nc localhost 30000
* [[cron]]
* rename command
    * `rename 's/.jpeg/.jpg/' *`
    * `rename -n 's/DSC/photo/gi' *.jpg`
    * `rename 'y/t,x,t/a,b,c/' *`
    * https://www.maketecheasier.com/rename-files-in-linux/
* `nproc` - Get number of processing units (cores) available
* [sshguard](https://www.sshguard.net/)
* dm-thin: A *Stackable* Linux device that reports more room/capacity that it
  actually has.  Then if the actual limit is reached, depend on the user for JIT
  addition of extra capacity
* Know if you are running wayland or x11:

  {{< highlight bash >}}
  loginctl show-session `loginctl|grep $(YOUR_USER_NAME)|awk '{print $1}'` -p Type
  {{< / highlight >}}

* [[Reverse SSH tunnelling]]
* `cpupower`: Manage processor power related configuration, enable/disable CPU
  frequency scaling, frequency governors
  * <https://www.kernel.org/doc/Documentation/cpu-freq/governors.txt>
* top/htop alterantives:
    * `glances` - <https://github.com/nicolargo/glances>
* sar/sadf: Monitor your system over time, find bottlenecks
    * <http://sebastien.godard.pagesperso-orange.fr/tutorial.html>
* VPN over SSH: <https://github.com/sshuttle/sshuttle>
* Collaborative tmux: <https://github.com/zolrath/wemux>
* TLDR client:
    * <https://github.com/dbrgn/tealdeer>
    * <https://github.com/raylee/tldr>
* [procs](https://github.com/dalance/procs) - Modern ps alternative
* [AlgoVPN](https://github.com/trailofbits/algo) - More secure, simpler VPN solution
* [diskus](https://github.com/sharkdp/diskus): More friendly and faster version of `du -sh`
* [ncdu](https://dev.yorhel.nl/ncdu): Disk Usage Analyser
* [Disk Usage Analyzer](http://www.marzocca.net/linux/baobab/baobab-getting-started.html)
* [grc](https://github.com/garabik/grc): Command Output Coloriser - written in python
* [hdparm](https://en.wikipedia.org/wiki/Hdparm): Show hard-disk/SSD related information
    * `hdparm -I /dev/sda`
* [[Power-related utilities]]
* [showfoto](https://kde.org/applications/graphics/org.kde.showfoto): Easy to use / not bloated image editor:
* [asciinema](https://asciinema.org/): Record and share your terminal sessions
