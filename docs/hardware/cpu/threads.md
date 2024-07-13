---
sidebar_position: 1
---

# Threads

## What are Threads?

Threads can be thought of as virtual sequences of instructions that are issued to a CPU,  
That a scheduler can manage independently.

Primarily, they’re a way to divide workloads and share those responsibilities among different processors.

three related terms are multitasking, multi-threading and hyper-threading.

Threads are crucial for multitasking,  
Allowing a single core to perform multiple tasks concurrently.

In multi-threading, tasks are split into distinct threads and run in parallel.

Hyper-threading helps achieve even greater performance benefits because processors are used to carry out two threads at the same time.

## What is Single-Threading

Single-threading is a process in which one command is executed at a time.

## What is Multi-Threading?

Multi-threading is a technique,  
Where a single application can be broken down into two or more sub-tasks,  
That can be processed simultaneously.

This is particularly useful in programs where certain tasks are independent of others and can be executed concurrently.  
Leading to more efficient use of the CPU’s processing power.

## How Does Multi-Threading Work?

Multi-threading works by allowing multiple threads to exist within the same process,  
Sharing the same resources but running independently of each other.

This allows for parallel processing,  
Where multiple tasks are executed at the same time.

The operating system allocates processing time to different applications and their individual threads.

This can enhance performance,  
By allowing the CPU to switch to another thread,  
While waiting for a response,  
Like from the user or a disk drive.

## What is Hyper-Threading?

Hyper-threading is a simultaneous multi-threading implementation developed by Intel,  
That allows each CPU core to run multiple threads simultaneously.

It allows each physical core to appear as two virtual cores in the operating system.  
The software uses available hardware resources more efficiently.

## References

- [aws.amazon.com/what-is/cpu/](https://aws.amazon.com/what-is/cpu/)
- https://shardeum.org/blog/cpu-cores-and-threads/
