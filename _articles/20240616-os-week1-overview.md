---
id: 1
title: "1. Operating Systems - Overview"
subtitle: "Introduction to Operating Systems"
date: "2024.06.15"
tags: "OS, Lecture"
---

This article is based on the COMP2006 Operating Systems lecture at Curtin University. It is intended for note-taking and providing a summary for other students. The actual lecture did not cover all of the content from the book and may differ in other semesters. This article is from semester 1 of 2024.

# Operating System
There is no universally accepted definition of `OS`, but we can say OS is a program that acts as an interface between a user and hardware. `Kernel` is part of OS, and it's running all the time on computer.

## Purposes
1. To provide an environment for user to execute program.
2. To simulate features not available on hardware such as Virtual Memory, Virtual Operating System
3. To control all the resources.

![image](/images/2024-06-16-15-37-14.png)

## Computer System Organization
`System Bus` is using for transferring all signals between CPU and other devices (I/O devices and Memory). And each `device controller` is in charge of particular device type and has local buffer.

To execute program, computer should store the program into its memory including Operating System as well. 

![bootstrap](/images/2024-06-16-18-02-28.png)[^1]


[^1] : Bootstrap Image from [Link](https://uselessetymology.com/2019/11/07/the-origins-of-the-phrase-pull-yourself-up-by-your-bootstraps/)

