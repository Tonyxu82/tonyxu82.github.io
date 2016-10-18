---
layout: post
title: Why Threads are a Bad Idea
author: Tony Xu
category: Operating System
description: Why event-driven design is better than thread-based desgin
---

The threads become popular, but even an expert will grumble that they are hard to program. The denouncement from John Ousterhost is extremely sharp. In his slide, he claims that the event-driven programming is a better choice for most purposes which the threads could be applied. For supporting this idea, he gives a brief introduction to the concepts of threads and events respectively, and comparing their pros and cons.

This presentation is made in 1995, so we have paid attention to the history context. At that time, the configuration of most personal computers and workstation were very poor (from today's perspective) - single CPU, single core, small memory and secondary storage. Some workstation and high performance computer can support multiprocessor, but the price cannot be accepted by the general consuming public.

In the author's opinion, the threads are a solution for the scenarios such as scientific computation, distributed systems, which need the concurrent mechanism. Under the skin, each of them is an independent instruction execution sequence, but share the state - memory, file and etc. They are scheduled in preemptive and synchronized by technique such as locks and conditions. Why is programming with threads hard? Why so few programmers can use them well? The author summarizes 8 reasons (with my understanding):

1. Synchronization - you need locks to protect the shared data from corruption caused by concurrently writing by the threads.
2. Deadlock - occasionally, different threads can interlock with each other for requiring certain shared resources locked by the peer.
3. Hard to debug - The context of a thread depends on the internal scheduling mechanism, which we cannot control manually.
4. The threads break abstraction - Abstraction separates the interface from the implementation and modules the system, it will let program more conveniently. But when we are using threads, we have to care about how to access data in lower-level implementation and decide to lock/unlock it, it prevents us for further abstracting.
5. Callbacks don't work with locks - the callback mechanism is we write logic and called by the other. If we have locked some shared data in our thread, and then trigger a callback to modify it, we will be deadlocked.
6. Hard to tunning to get a good performance - Is a team always better than a single person? Not really, if the task cannot be well divided and cooperated among the team member, the result will be a catastrophe. For the multi-thread, the situation is the same. We have to mention that the scheduling and context switching will bring negative impact on performance, especially in the uni - processor machine.
7. The threads are not well supported from systems and tools - in 1995, the situation was true.
8. Concurrency is not necessary in many ways - In 1995, most of the PCs and workstation were still uni-processor and small memory machine, author's opinion was partially true at that moment. But today, the multi-core has been a standard configuration for PC even handheld device, to adapt a system to hardware development to get more power from concurrency is necessary.

The event-driven is a programming paradigm for certain systems/subsystems, such as GUIs and distributed systems, reacting to an external request and sending the response. In these systems, it always exists a loop for listening and dispatching the incoming events. If any one interest in certain events, you can write a callback like procedure, and register it in the system. If this kind of events comes, you will receive it and be called for handling it. Taking Win32 GUIs programming, for example, if we want to react a click of some button in the dialog, we can overload OnButton () callback method and register it to react the event by clicking that button. If the button has been clicked, an event will be sent and OnButton () will be called by the system, and our logic will be executed. Although the author claims the event-driven programming can replace thread in most of situations, but event-driven has its obviously limitation for certain kinds of system paradigms and drawback to get better performance when on multiprocessor or multicore environments. Another paradox, hard to be bypassed, is that threads are widely used in in many event-driven architect distributed systems. A telecommunication system is a typical example of annotating this paradox, it always keeps pre-allocated thread pool, and when an event comes, the dispatcher route this event to a dedicated handler, the system take an idle thread from the pool for executing the logic of the handler for improving concurrent performance to bring a better experience for users.

In this slide, the author will summarize the drawback of programming with threads, and claim the event-driven paradigm is a better choice in most of the situations. If we put ourself in 1995, maybe I will support the author's idea. But nowadays, the development of hardware let the true concurrency computer system be cheap, and the system and tool ameliorate a lot for supporting threads. For using this facility, we have to embrace threads. Even though, programming with thread is still a tough work, the summary in this slide is still useful for avoiding the pitfall and trap in front of you.