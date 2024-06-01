---
id: 0
title: "5. Operating System : Memory Management"
subtitle: "Continuous Memory Allocation"
date: "2024.05.24"
tags: "OS, Paging"
---
# Continuous Memory Allocation
Continuous memory allocation assigns a process to a contiguous block of memory, ensuring that all memory addresses used by the process are sequential. This method is simple to implement but can lead to inefficient memory use due to fragmentation. Common strategies for this allocation include first-fit, best-fit, and worst-fit approaches. To manage fragmentation, compaction may be required to consolidate free memory spaces.

## Swapping
Removed processes are not currently using from memory, and move them to secondary storage. And then, load new process into new empty space.

![1](/images/2024-06-01-14-57-21.png)

### Advantage
If required memory space from several processes is higher than actual memory size, we can execute several processes at the same time.

## Concept of Continuous Memory Allocation
Process need to be allocated in empty space of memory. There are few ways to implement it.

**First-Fit**
