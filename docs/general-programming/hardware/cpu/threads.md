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

## What is Single-Threading?

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

## Notes

CPUs come in many different varieties, such as single-core, dual-core, quad-core, and multi-core processors. The more cores a processor has, the faster it can carry out tasks.

In addition to executing instructions from programs, the CPU also manages other components of the system like RAM (random access memory), HDD (hard disk drive), or SSD (solid-state drive).

The CPU is responsible for coordinating and communicating with the other components.

The CPU is responsible for coordinating and communicating with the other components. It’s important to choose the right CPU, depending on what types of tasks you plan to do.

Your CPU is likely to be different if you’re running applications and workflows vs storing archives and legacy files. CPUs vary widely in performance, power consumption, and cost. The activities the CPU performs will materially impact the right choice for your business needs and budget.

CPU Cores
The number of cores in a system will determine how many programs and tasks it can execute at once. For instance, a single-core processor may be able to handle one task at a time. By contrast, a quad-core processor could handle up to four simultaneous tasks. As the number of cores increases, so do processing speed and throughput.

Single-Core CPU
Single-core CPUs are cheaper than multi-core CPUs, and they consume less power. This makes them great options for laptops, tablets, and other mobile devices. They also work well if the tasks you need to complete are relatively simple or don’t require too much multitasking. On the other hand, they will lack the performance of a multi-core CPU.

Multi-Core CPU
A multi-core CPU is ideal for multitasking and running applications that require high levels of performance or processing large datasets. This type of processor can divide tasks among the cores, allowing each to handle its own piece. A multi-core CPU will require more energy and supporting hardware to support its power.

There are two common approaches to multithreading:

Parallel multithreading. Also known as true multithreading, this lets the processor core handle two or more threads simultaneously.
Concurrent multithreading. This is a modification of single-threading where the processor core only handles one thread at a time but timeshares the processor between multiple threads, letting the processor handle more than one thread at a time.

There are also numerous types or models of multithreading, coordinating and processing multiple threads in various ways. For example, some types of multithreading will enforce equal time slices to divide processor time equally, while other approaches can vary time slices according to thread priority or other criteria. Common types of multithreading include the following:

Pre-emptive.
Cooperative.
Coarse grained.
Interleaved.
Simultaneous.
Many to many.
Many to one.
One to one.

## multithreading and multiprocessing

Finally, there is a difference between multithreading and multiprocessing. Where multithreading allows the same CPU to process or appear to process two or more threads simultaneously, multiprocessing simply adds additional CPUs to handle more processes and threads, effectively using brute force to improve software performance. Most modern processors provide more than one core, so performance-sensitive software is increasingly leveraging the availability of additional cores to support greater parallelism in software execution.

Cores are physical processing units.
Threads are virtual sequences of instructions given to a CPU.
Multithreading allows for better utilization of available system resources by dividing tasks into separate threads and running them in parallel.
Hyperthreading further increases performance by allowing processors to execute two threads concurrently.

Modern processors support hyperthreading, a technology that allows one physical core to be divided into two virtual cores, thus allowing the CPU to work on multiple threads of execution simultaneously. This increases system performance by improving the utilization of available resources and increasing throughput.

## References

- [aws.amazon.com/what-is/cpu/](https://aws.amazon.com/what-is/cpu/)
- [shardeum.org/blog/cpu-cores-and-threads/](https://shardeum.org/blog/cpu-cores-and-threads/)
- [liquidweb.com/blog/difference-cpu-cores-thread/](https://www.liquidweb.com/blog/difference-cpu-cores-thread/)
- [techtarget.com/whatis/definition/thread](https://www.techtarget.com/whatis/definition/thread)
- https://www.backblaze.com/blog/whats-the-diff-programs-processes-and-threads/
- https://medium.com/@rodbauer/understanding-programs-processes-and-threads-fd9fdede4d88
- https://en.wikipedia.org/wiki/Thread_(computing)
- https://www.computerhope.com/jargon/t/thread.htm
