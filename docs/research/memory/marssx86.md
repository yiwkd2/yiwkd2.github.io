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

---

### Notes 06/13

- there are two different namespace for L1M, L2M. I don't think we need two.
- I want to move DRAMsim3 fold in marss folder, and completely integrate marss and DRAMsim3.
- In order to implement memory controller logic for hybrid memory system, I need to have better understanding about DRAMsim3 and memory system.

date: 06/13

---

### Notes 04/27

Questions
- How to calculate DRAM memory size from config files.
- How to measure bandwidth of each memory.
- How to decide ROI of benchmark.<br>
ptlcall_switch_to_sim(), ptlcall_switch_to_native() are called by benchmark.
some benchmark calls these directly from ptlcalls.h and others bind these with benchmark specific functions.
check ptlcalls.h (modified: 04/28)
- How to build benchmark and create disk image.<br>
 this is not an issue. check marss, each benchmark offical website (modified: 04/28)

**Todo**
- implement migration engine and find a way to record migration overhead.

date: 04/27

---

### Regarding DRAMsim3

I just finished reproducing plugging DRAMsim3 into Marssx86 and upload on my private github repo.<br>
I found few things I need to check carefully.<br>
1. the clock rate of l1m is 1.0GHz and that of l2m is 1.2GHz. is this a mistake?
2. is_full function of memoryController is not implemented for two tiered memory system.
3. all memory access is changed to read operation.

date: 04/27

3. write-back from LLC needs to be a write operation for DRAMsim3.
However, simple write miss should be a read operation for DRAMsim3 because of write-allocate policy.

modified: 04/28

---

### Debugging

[marssx86 official website](http://marss86.org/~marss86/index.php/Getting_Started) describes how to run simulator under gdb.<br>
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

date: 04/27

.gdbinit file
```
handle SIGUSR1 SIGUSR2 noprint nostop
b ptlsim/build/core/ooo-core/ooo-pipe.cpp:104
run -m 16384 -hda /home/youngin/research/memory/images/ubuntu-spec.img -simconfig sim.cfg -redir tcp:7001::22 -nographic
```

Whenever I use gdb for this project, I edit second line of .gdbinit file to set initial breakpoint.<br>

modified: 05/05


---

### qemu version conflict

the original [source code](https://github.com/donggyukim/Marssx86) has a build erorr caused by deprecated qemu functions.
I fixed it and uploaded it on my github private repo.

date: 04/27
