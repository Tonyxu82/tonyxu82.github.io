---
layout: post
title: An Introduction to Programming with Threads
author: Tony Xu
category: Operating%20System
description: A review of Andrew Birrell's paper - An Introduction to Programming with Threads
---

# Introduction

The concurrent mechanism is widely used in the modern systems, including operating systems, distributed system and so on. We can gain the benefits from it This paper concerns about how to use this mechanism by programming with threads. The author provides us introductory level content including:
1) The motivation of concurrency and the thread
2) The design of a thread facility
3) How to use such facility. What difficulties and pitfalls you will meet when using multi-thread.
4) Some principles for building a programming using threads.

# Edition and Credibility

The author, Andrew D. Birrell is principal researcher at Microsoft and has 40 years research experience in the general areas of operating systems and distributed systems[1].

The original paper published in 1989, which is based on the outcome of Digital's Systems Research Center (SRC). The programming language used in the paper is Modula-2. For more information about this language you can find in [2][3]. Actually, you can find a revision of it which keeping the original framework, but replacing the Modula-2 to C# [4]. The updated edition of it has been cited by 233 times in Google Scholar.

# Summary

In the paper, the author thinks the concurrent programming is an important skill at present, since you can benefit from up-to-date hardware facilities (multiprocessor, mutlicore, GPU) to get better performance, to deal with slow devices (secondary storage or network) and providing a better user experience. This is why we will introduce multi-processor and multi-thread facilities into the operating system. Comparing the processors, the cost of maintaining threads is relatively low, this is why we call it lightweight. But the multi-thread is not an elixir can let your system run concurrently at once, what you will face is the tough work to deal with the complexity and pitfall when you program with it. Author provide an introduction for the design of a thread facility, and how to use it and what you have to pay attention to, finally the he give some principles for the design and implementation of your program.

The basic facility of a thread includes the operations to maintain the life of a thread such as creation (fork), waiting for the other thread to finish the job (join) and alert, and the mechisam for sychnoization such mutex, monitor and condition variable (semaphore?). Then the paper gives a detailed description on how to use those operations. The logic of the author for each kind of operations is raising a problem, solving the problem and giving pitfall you have to pay attention when using it. The pitfall here, including the deadlock, starvation and performance degradation.

For better using concurrent programming, you will not only just learn how to use those techniques but also know some principles. Your program must be useful, such as your interface can be used in multiple thread's environment that means the every enter point must be thread re-entrant. The correctness more import and the performance, do you like to run faster and faster in the wrong direction? Based on those two points above, then we will avoid the deadlock to keep the program alive and use resources efficiently.

# Reference
1. http://research.microsoft.com/en-us/people/birrell/
2. http://www.modula2.org/tutor/index.php
3. http://en.wikipedia.org/wiki/Modula-2
4. Birrell, Andrew D. An introduction to programming with C# threads. Technical report, Microsoft Corporation, May 2003. Manuscript available at http://research. microsoft. com/~ birrell/papers/ThreadsCSharp.pdf, 2003.
