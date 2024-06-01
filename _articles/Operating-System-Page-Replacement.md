---
id: 2
title: "7. Operating System : Memory Management"
subtitle: "Page Replacement and Allocation of Frames"
date: "2024.05.24"
tags: "OS, Paging"
---
# Demand Paging
Demand paging is a memory management technique used by operating systems to optimize memory usage. In demand paging, only the required pages of a program are loaded into memory when needed, rather than loading the entire program at once.[^1]

**Process**
1. Page Request: The CPU requests a specific page needed to execute the current instruction.
2. Page Table Lookup: The CPU checks the page table to see if the requested page is in physical memory.
3. Page Table Check: If the page is present, the CPU continues execution; if not, a page fault occurs.
4. Page Fault Handling: The operating system loads the requested page from secondary storage into memory and updates the page table.
5. Resuming Execution: The CPU resumes execution with the now-loaded page, continuing the interrupted process.

**Pure Demand Paging** : Pure demand paging is a memory management technique where pages are loaded into memory only when accessed. Initially, no pages are in memory. When a page is accessed, a page fault occurs, prompting the operating system to load the needed page from the disk. This method conserves memory but can cause performance overhead due to frequent page faults.

# Page Replacement Algorithms
When we are allocating pages on memory, memory will be full. Therefore, some of the pages need to be replaced. Then, how can we decide which page should be replaced?

## What are key elements to determine good algorithm?
**Algorithm that has less page fault** (higher page fault rate will decrease computer's performance).
We can investigate occurences of page fault by using `page reference string`. Page reference string is the string that skipped the continuous page. For example, the page string has `2 2 2 3 5 5 5 3 3 7` than page reference string will be `2 3 5 3 7`.

## FIFO Page replacement algorithm
The FIFO page replacement algorithm is one of the simplest page replacement algorithms. It works on the principle of "First-In-First-Out," meaning that the oldest page in memory is replaced first when a new page needs to be loaded.

### Example

1. Consider a sequence of page references: 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5.
2. Assume the memory can hold 3 pages at a time.

| Step | 1  | 2  | 3  | 4  | 5  | 6  | 7  | 8  | 9  | 10 | 11 | 12 |
|------|----|----|----|----|----|----|----|----|----|----|----|----|
| **Page Reference** | 1  | 2  | 3  | 4  | 1  | 2  | 5  | 1  | 2  | 3  | 4  | 5  |
| **Memory State**   | 1  | 1  | 1  | 4  | 4  | 4  | 5  | 5  | 5  | 5  | 4  | 4  |
|                    | -  | 2  | 2  | 2  | 1  | 1  | 1  | 1  | 1  | 3  | 3  | 5  |
|                    | -  | -  | 3  | 3  | 3  | 2  | 2  | 2  | 2  | 2  | 2  | 2  |
| **Page Fault**     | Yes| Yes| Yes| Yes| Yes| Yes| Yes| No | No | Yes| Yes| Yes|

### Pros and Cons
The optimal page replacement algorithm is beneficial when memory needs to run specific pages quickly when a program is loaded. However, it has disadvantages when there are pages that need to be executed the whole time while the program is running.

## Second-Chance Page Replacement Algorithm
The second-chance page replacement algorithm is a variation of the FIFO page replacement algorithm. It works similarly to FIFO but also considers the reference bits in the Page Table Entries (PTE).

If the reference bit is 1, the page is given a second chance. If the reference bit is 0, the page will be replaced. When the CPU refers to the page, the page's reference bit is set to 1.

## Optimal Page replacement algorithm
The optimal page replacement algorithm, also known as Belady's algorithm, replaces the page that will not be used for the longest period of time in the future. It is theoretical and cannot be implemented in practice because it requires future knowledge of the reference string. However, it serves as an ideal benchmark to compare the performance of other page replacement algorithms.

### Example

1. Consider a sequence of page references: 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5.  
2. Assume the memory can hold 3 pages at a time.

| Step                | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   |
|---------------------|------|------|------|------|------|------|------|------|------|------|------|------|
| **Page Reference**  | 1    | 2    | 3    | 4    | 1    | 2    | 5    | 1    | 2    | 3    | 4    | 5    |
| **Memory State**    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    |
|                     | -    | 2    | 2    | 2    | 2    | 2    | 2    | 2    | 2    | 2    | 2    | 2    |
|                     | -    | -    | 3    | 4    | 4    | 4    | 5    | 5    | 5    | 3    | 3    | 3    |
| **Page Fault**      | Yes  | Yes  | Yes  | Yes  | No   | No   | Yes  | No   | No   | Yes  | Yes  | No   |

### Pros and Cons
This algorithm gaurantees that minimum page fault rate. However, it cannot be implemented in practical. Since, we cannot predict the future correctly. This is useful only for measurement.

## LRU Page replacement algorithm
The LRU (Least-Recently-Used) page replacement algorithm is conceptually similar to the optimal page replacement algorithm. However, the LRU algorithm replaces the page that has not been used for the longest time, rather than predicting which pages will not be used for the longest time.

### Example:
1. Consider a sequence of page references: 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5.
2. Assume the memory can hold 3 pages at a time.

| Step                | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   |
|---------------------|------|------|------|------|------|------|------|------|------|------|------|------|
| **Page Reference**  | 1    | 2    | 3    | 4    | 1    | 2    | 5    | 1    | 2    | 3    | 4    | 5    |
| **Memory State**    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    |
|                     | -    | 2    | 2    | 2    | 2    | 2    | 2    | 2    | 2    | 2    | 2    | 2    |
|                     | -    | -    | 3    | 4    | 3    | 3    | 5    | 1    | 1    | 3    | 4    | 5    |
| **Page Fault**      | Yes  | Yes  | Yes  | Yes  | No   | No   | Yes  | No   | No   | Yes  | Yes  | No   |

# Thrashing and Frame Allocation
The main reason why the page fault rate is high can be due to using a poor page replacement algorithm and having a low number of frames. Thrashing occurs when the system spends more time paging than executing processes. In the context of multiprogramming, if we run too many processes at the same time, the CPU will spend more time on page replacement. Thrashing occurs because we did not guarantee the minimum number of frames needed by each process.

## Equal Allocation
This is the simplest allocation. The basic idea is to give an equal number of frames to each process. However, this approach is not recommended because the size of each process can vary significantly. For example, allocating the same number of frames to a large process like League of Legends and a small process like Notepad is not rational.

## Proportional Allocation
Thus, processes size needs to be considered. The proportional allocation allocates a frame to each processes based on its size. It is also called as a static allocation. This method is also not perfect way, since some of the processes size are big, but actual frame needs are smaller. And also, process size is small, but they can need more frames.

## Working Set Model
The working set model checks the CPU's page referencing rate over a specific period and allocates frames based on that rate. 
- Monitor Page References: The model tracks the set of pages that a process references within a fixed time window or working set window.
- Adjust Frame Allocation: Frames are allocated dynamically to each process based on the number of pages in its working set, ensuring each process has enough frames to avoid frequent page faults.
- Reduce Thrashing: By ensuring each process has the necessary frames for its current working set, the model helps reduce thrashing and improve overall system performance.

To get working set model, we need pages referenced by the process, and time interval.

## Page Fault Rate Allocation
a


[^1]: [What is Demand Paging in OS (Operating System) | DataTrained](https://datatrained.com/post/demand-paging-in-os/)