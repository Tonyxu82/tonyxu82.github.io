---
layout: post
title: On the Duality of Operating System Structures
author: Tony Xu
category: Operating System
description: A paper review of "Lauer, Hugh C., and Roger M. Needham. "On the duality of operating system structures." ACM SIGOPS Operating Systems Review 13.2 (1979) 3-19.".
---

This review is based on the paper "Lauer, Hugh C., and Roger M. Needham. "On the duality of operating system structures." ACM SIGOPS Operating Systems Review 13.2 (1979): 3-19.".

Event-Driven Model (Message Oriented Model) or Multi-Thread Model (Procedure Oriented Model)? The arguments always exist in design in large software system such as operating systems. In this paper, the authors try to reconcile such conflict to make the system design area to be more rational.

In the authors' opinion, Event-Driven Model and Multi-Thread Model is interchangeable. Although, this idea is made based on their experience not rigid formalism, they follow a logical routine:

1. Giving the some description about characteristics of Event-Driven Model and Multi-Thread Model.
2. The authors construct canonical models (abstract model) for each design ways for the comparing purpose.
3. Comparing these two models and establishing an item to item mapping between them.
4. To Show there is little impact on the performance between these two models
5. Giving more support evidence of their experience for their ideas
6. The models are equivalent, but computer architecture and development environment can affect the decision for choosing the model.
7. Conclusions

From the perspective of the engineering field, their method works, since many knowledge are gained from practical experience.

Firstly, they characterize these two models. Comparing the Multi-Thread Model, they think an Event-Driven Model has
1. Smaller amount of processes (threads), but the logic of each process (thread) is more complex; the
2. Smaller amount of directly shared data since it use message channels for communication not those data and the locks.

In the next part, For each model, they summarize the requirements, good design practice, the hallmark of a successful system, and detailed canonical model. This part is very Instructive for whom design system.
The Canonical Model for Event-Driven:

1. Message: A data structure used for sending information
2. Message Body: The context of the message
3. Message Identifier: A handle for the massage, you can operate the message with this handle.
4. Message Channel: A abstract structure for representing the destination of the message.
5. Messgage Port: A queue located in the target process. Before we can use a message channel, we shall bind the port to it. A port can be binded by several channels.
6. SendMessage (Message Channel, Message Body) returns Message Identifier.
7. AwaitReply (Message Identifier) return Message Body
8. WaitForMessage (Set of Message Port) return Message Body, Message Identifier and Message Port
9. SendReply (Message identifier, Message Body)

The Canonical Model for Multi-Thread:

1. Procedures: A segment of code (including algorithms), local data, parameters and the return values.
2. Synchronous Procedure Call: Call and wait for return.
3. Asynchronous Procedure Call: Fork and Join
4. Module: Like the "class" used in Object-Oriented Language, it is a set of data and procedures. The access of elements in this set can be controlled by the "private" and "public" attracted to them. If they have been set to public, it means they can be accessed by the external procedures, else they can only be used inside of the module.
5. Module Instantiation: Like the object generated from class in the Object-Oriented Language.
6. Condition Variable: A part of the Monitor, used for synchronization purpose. There are two main procedures:
-.Wait Condition Variable: Let the threads wait for the lock to be released
-.Signal Condition Variable: If the lock has been unlocked, notify the queued threads.

Comparing Event-Driven Model and Multi-Thread Model, we can map their canonical model item by item like below:

Event-Driven Model|                Multi-Thread Model
-------------------------|-----------------------------------
Process|                           Module
CreateProcess|                     Monitors New/Start
Message Channel & Port|            Procedure Identifer
SendMessage&AwaitReply (Immediate)|   Syncnoizating Procedure Call
SendMessage&AwaitReply (Delayed)|    Asycnoizating Procedure Call Fork, Join
SendReply|                         Return
WaitForMessage|                    Lock
Case, Arms of the Case statement selective|   Entry Attributed, Entry Procedure Declarations.
Waiting For Message|               Condition Variables, Wait, Signal

This mapping relationship shows this two model can be logically interchangeable. But do they have same performance? The authors give a criteria to measure for the performance of a system of programs

1. The execution time
2. Computational overhead, including scheduling and dispatching.
3. The queuing and waiting times.

For execution time, the authors test it in GEC4080 and MESA, they imply that the result is no difference in an obscure way; For the conditions for scheduling and dispatching, the author think both conditions are the same; The author also thinks if an event should wait for a dedicated resource to be released in Event-Driven Model, the same situation (waiting for locked resource) will happen in  the Multi-Thread Model. So authors think there is no penalty when using either model.

Although, the authors try to prove these two models are equivalent, but they also admit that the computer architecture and development environment will affect the choice made by designers. The essential rule is which model is more convenient for implementing. They want to persuade the operating system designers to eliminate obstinacy and adopt more sensible solution. They also want to create a uniform way to design systems based on the both ways.

Nowadays, these two kinds of models are always to be used in hybrid ways in the design of operating systems and distributed systems. In my previous project, there is dispatcher for receiving the messages (or events). This dispatcher will route the message to dedicated handler according to the message type and the id.  The handler is not a single thread, actually, is a thread pool, each time a new message comes, it will pick a thread from the pool and assign that message for it. In the UML, it has already unified the design of systems based on these two ways. When you use sequence diagram, to draw the invoking relationship between caller and callee, you will find to call a procedure or to send an event is undifferentiated.
