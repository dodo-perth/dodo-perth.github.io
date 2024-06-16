---
id: 1
title: "1. Operating Systems - Overview"
subtitle: "Introduction to Operating Systems"
date: "2024.06.15"
tags: "OS, Lecture"
---

This article is based on the COMP2006 Operating Systems Lecture at Curtin University. It is intended for note-taking and providing a summary for other students. The actual lecture did not cover all the content from the book and may differ in other semesters. This article is from semester 1 of 2024.

# Operating System

There is no universally accepted definition of an operating system (OS), but we can describe an OS as a program that acts as an interface between the user and the hardware.

## Purposes

1. To provide an environment for the user to execute programs.
2. To simulate features not available in hardware, such as virtual memory and virtual operating systems.
3. To control all the resources.

![image](/images/2024-06-16-15-37-14.png)[^1]

## Computer System Organization

The system bus is used for transferring all signals between the CPU and other devices (I/O devices and memory). Each device controller is responsible for a particular device type and has a local buffer.

To execute a program, a computer must store it in memory along with the operating system. When powered on, the computer needs an initial program (bootstrap) to start running. This bootstrap program is stored in ROM or EEPROM, which are non-volatile storage types.

![image](/images/2024-06-16-18-02-28.png)[^2]

The kernel is the core component of an operating system that manages system resources and facilitates communication between hardware and software. It runs continuously. In Linux, the first system process is `init`, which is also called by the bootstrap program.

The operating system is interrupt-driven, a significant concept for understanding further theory. Being interrupt-driven means that the operating system remains idle until an interrupt occurs from hardware or software (system call).

## How the CPU Works with Interrupts

1. **Receive Interrupt:** The CPU receives an interrupt signal from hardware or software.
2. **CPU Stops Current Activity:** The CPU stops its current execution and saves its state.
3. **Execute Interrupt Service Routine (ISR):** The CPU jumps to a predefined memory location to execute the Interrupt Service Routine (ISR), which handles the interrupt.

## Role of the Interrupt Vector Table
The interrupt vector table provides the address of the appropriate Interrupt Service Routine (ISR) for each interrupt, allowing the CPU to efficiently determine and execute the correct ISR when an interrupt occurs. The interrupt vector table contains vector numbers (0-255) and descriptions. It is not necessary to memorize the table, but it is important to understand that lower numbers have higher priority.

For example, if a vector number 14 (page fault) interrupt occurs and the CPU is working on its ISR, and during that process, a vector number 1 (debug exception) makes a system call, the CPU will stop the ISR for vector 14 and jump to the ISR for vector 1.

[^1]: [Operating System Purposes Image](https://www.geeksforgeeks.org/introduction-of-operating-system-set-1/)
[^2]: [Bootstrap Image](https://uselessetymology.com/2019/11/07/the-origins-of-the-phrase-pull-yourself-up-by-your-bootstraps/)
