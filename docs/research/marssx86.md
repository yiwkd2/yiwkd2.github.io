---
layout: default
title: Marssx86
parent: Memory
grand_parent: Research
---

# Marssx86
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 2021

### Debugging

[marssx86 official website](http://marss86.org/~marss86/index.php/Getting_Started) describes how to run simulator under gdb.

first we need to build simulator with debug option

```
$ scons -Q debug=1
or
$ scons -Q debug=2
```

and then run under gdb with these commands

```
$ gdb qemu/qemu-system-x86-64
(gdb) handle SIGUSR1 SIGUSR2 noprint nostop
(gdb) run -m ~~
```

this process can be automated by creating .gdbinit file in the project repo.

I just created .gdbinit only contains handle command because I need to set breakpoint manually
before run the simulator.<br>
GDB has an auto-load safe for security reason, so I created ~/.gdbinit file as shown below.
```
set auto-load safe-path /
```

I wanted to automate runing with arguments, hence this is not a good solution for that.

### qemu version conflict

the original [source code](https://github.com/donggyukim/Marssx86) has a build erorr caused by deprecated qemu functions.
I fixed it and uploaded it on my github private repo.

date: 04/27




