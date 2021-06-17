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


