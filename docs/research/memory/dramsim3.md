---
layout: default
title: DRAMsim3
parent: Memory
grand_parent: Research
---

# DRAMsim3
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Basic Concept

### Total size of the Memory System

Total size = (# of channels in system) * (# of ranks per channel) * (# of banks per rank) * <br>
(# of rows per bank) * (# of columns per row) * (# of bytes per column)

last two terms can be replaced by (# of bytes per cacheline) * (# of cacheline per row) <br>
because (# of cacheline per row) can be calculated as follows <br>

(# of cacheline per row) = (# of columns per row) * (# of bytes per column) / (# of bytes per cacheline)

## DRAMsim3

### CalculateSize()

this function calculates # of ranks<br>

```
devices_per_rank = bus_width / device_width;
```
devices_per_rank represents # of chips on one side of DRAM

```
int page_size = columns * device_width / 8;
int megs_per_bank = page_size * (rows / 1024) / 1024;
```

page_size is page size in bytes, megs_per_bank is the size of each bank in MB.

```
int megs_per_rank = megs_per_bank * banks * devices_per_rank;
```

banks is bankgroups * banks_per_group, therefore megs_per_rank is the size of each rank in MB.

```
ranks = channel_size / megs_per_rank;
channel_size = ranks * megs_per_rank;
```

ranks is # of ranks per channel.<br>

### DDR4_8Gb_x8_3200.ini

Based on the above understanding, I'm going to calculate the total # of ranks in this system.

```
[dram_structure]
protocol = DDR4
bankgroups = 4
banks_per_group = 4
rows = 65536
columns = 1024
device_width = 8
BL = 8

...

[system]
channel_size = 16384
channels = 1
bus_width = 64
```

devices_per_rank = 64 / 8 = 8
page_size = 1024 * 8 / 8 = 1024 (page size is 1KB)
megs_per_bank = 1024 * (65536 / 1024) / 1024 = 64 (bank size is 64MB)
megs_per_rank = 64MB * (4 * 4) * 8 = 8192MB (rank size is 8GB)
ranks = 16384 / 8192 = 2 (# of ranks in this channel is 2)

Thus, this system has 1 channel, 2 ranks in this channel whose size is 8GB.
Is the size of this system 16GB? why does file name say its size is 8GB?
