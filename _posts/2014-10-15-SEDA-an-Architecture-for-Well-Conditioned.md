---
layout: post
title: SEDA an Architecture for Well Conditioned
author: Tony Xu
category: Operating System
description: This review is based on the paper "Welsh, Matt, David Culler, and Eric Brewer. "SEDA an architecture for well-conditioned, scalable internet services." ACM SIGOPS Operating Systems Review. Vol. 35. No. 5. ACM, 2001".
---

This review is based on the paper "Welsh, Matt, David Culler, and Eric Brewer. "SEDA: an architecture for well-conditioned, scalable internet services." ACM SIGOPS Operating Systems Review. Vol. 35. No. 5. ACM, 2001".

Facebook, Google, Twitter... These services are supported million and even 10 million users' requests every day. If they want to provide better service, it means they must be designed and implemented to be high availability, robust and responsive. The challenge of satisfying these requirements are

1. The service has become more complex for getting better user experience.
2. For rapid react user's requirement, the service logic changes fast.
3. The platform for hosting service must support a wide range of services not specific one.

To meet the requirements and challenges above, the authors of this paper propose a new architecture SEDA(staged event-driven architecture). The design goal of it includes:

1. The framework is designed for general service for supporting scalability.
2. Handling highly concurrency, in other words higher throughput and lower latency.
3. Supporting dynamic overload control. Even in extreme high load condition, it still can maintain certain throughput.

The SEDA absorbs the merits of others, developing model - thread based concurrency, thread pool and event-driven concurrency. For easy developing and tuning, it has been designed as a set of building blocks - stages. Those stages have input queue and outputs, so you can connect them conveniently to construct a new service and also provide a certain level of errors segregation. For a stage, there is an event-driven framework, and a thread pool for handling dispatch events. There are two controllers in each state to provide dynamic feedback control mechanism, one can measure the length of input queue for adjust the size the thread pool, and the other can evaluate the out rate of it for predicting the performance of adjacent stages and change its processing rate. In the testing (Figure8, 9) shows these two kinds of controller work very well.

Comparing to the thread-based concurrency and thread pool model, SEDA's dynamically scalable thread pool according to feedback control can avoid overheads caused by cache missing, scheduling lock, unfairness and the difficulties in determining the bottleneck. Comparing to the event-driven model, it can increase the concurrent capability and avoid the wrong assumption made in event model - assuming the event handle process will not be blocked.

The concept of SEDA has already been used in Sandstorm, an internet services platform. In sandstorm, SEDA has been applied to implement a asynchronous socket I/O and file I/O. The other applications include Haboob, a http server and Gnutella peer-to-peer file sharing network.

Since in stage, an adoptive overload control mechanism has been applied, so two new challenges have been raised, one is what conditions can be determined to be overload. The other is what strategy we can apply to the situation of overload.

For me, the most interesting ideas in this paper are

1. Pipeline design of architecture.
2. The overload control mechanism used in SEDA.

I think this kind of architect is a inborn distributed system, actually it has already been applied into some telecommunication systems for scalability, perforamce ad high availibiy purpose. The algorithm and strategy used in overload control mechnism of SEDA is too general, more information have to be provided.
