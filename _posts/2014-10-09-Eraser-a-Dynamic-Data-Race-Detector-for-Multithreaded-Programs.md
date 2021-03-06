---
layout: post
title: Eraser a Dynamic Data Race Detector for Multithreaded Programs
author: Tony Xu
category: Operating System
description: a paper review of "Savage, S., Burrows, M., Nelson, G., Sobalvarro, P., & Anderson, T. (1997). Eraser a dynamic data race detector for multithreaded programs. ACM Transactions on Computer Systems, 15(4), 391¨C411. doi:10.1145/265924.265927 "
---

The review is based on the paper of "Savage, S., Burrows, M., Nelson, G., Sobalvarro, P., & Anderson, T. (1997). Eraser: a dynamic data race detector for multithreaded programs. ACM Transactions on Computer Systems, 15(4), 391¨C411. doi:10.1145/265924.265927 "

Nowadays, multithread is common but hard to program, even for an expert. One of the reasons is sychnoization. And the data race (race condition) is one of critical problem in sychnoization. The data race is two concurrent threads access a shared variable and at least one of them tries to modify it, and the result is timing-dependent. The potential data race, especially when the read/write order are not expected will corrupt the shared data. If this data is your account balance, that will be a disaster. Traditionally, we use lock & locked methods to protect such shared data, which we can call it critical section. But the problem is sometimes we will forget to protect the critical section since the complexity of the logic of the program. How to detect data race dynamically and statically become crucial.

For solving the problem above, the authors propose an approach, based on Dinning and Schonberg's work [3], which following the routine of Lamport's happen-before method, to detect data race dynamically. The core of this approach is an algorithm "Lockset". The essence of this algorithm is to follow the locking discipline and compare the set of locks which the program should have for protecting the critical section and set of locks the program actually have. If the latter set is not the subset of the former, it means some shared variables have not been well protected. The Eraser is a program based on this method for detecting dynamic data race in the binary program (implemented based on ATOM, with some techniques used by debug program, such as shadow memory). It assumes the data in the heap and data section (not including stack) as possible shared variable, then how many locks a program should have will be determined based on the checking result on such variables. Then, it monitors the execution of the program, to compare the actual set of locks used, if there is a shared variable no longer protected by the lock, then an alarm will be raised. In some cases, such as memory resource, private locks and benign races, false alarms will be given, The Eraser will also provide an annotation mechanism for suppressing them. Currently, the Eraser still has a serious performance problem by slowing down the program by a factor 10 to 30, and the locking discipline used in it is too strict. But the experience in AltaVista, Vesta Cache Server, Petal and undergraduate coursework shows it works well. In the future version, author want to improve it by updating ATOM for improving performance, and support read-write locks, multiple locks and deadlock detection.

The authors' work is essentially based on the Lamport's Happen-Before. In Lamport's method, the order of events A and B is a partial order; which means they cannot change their position in the sequence. The order decides result when events try to modify the shared variables, if some shared variables are not locked; the happens-before approach will miss this data race. For me, I have not read the Lamport's original paper, whether there are timestamps for each event to guarantee such an order? Compared to the Lamprt's work, the authors' method is based on "detects violations the locking discipline, not races"[4], that means it can detect potential race conditions may never happen. As the authors said, the Lamport's work can deal many synchronization situations, but the genertility also bring the higher cost, so the narrower the focus to the lock method commonly used in modern days, this means the implementation simpler, cheaper and more efficient.

In this paper, when mentioning the performance and correctness, the authors are always equivocation. It's maybe the biggest problem of this paper.

Reference:

1. LAMPORT, L. 1978. Time, clocks, and the ordering of events in a distributed system. Commun. ACM 21, 7 (July), 558¨C565.
2. HOARE, C. 1974. Monitors: An operating system structuring concept. Commun. ACM 17, 10 (Oct.), 549¨C557.
3. DINNING, A. AND SCHONBERG, E. 1991. Detecting access anomalies in programs with critical sections. In Proceedings of the ACM/ONR Workshop on Parallel and Distributed Debugging.
ACM SIGPLAN Not. 26, 12 (Dec.), 85¨C96.
4. David Mazi¨¨res, Stanford CS240:Advanced Topics in Operating Systems notes. http://www.scs.stanford.edu/06au-cs240/notes/l5d.txt
