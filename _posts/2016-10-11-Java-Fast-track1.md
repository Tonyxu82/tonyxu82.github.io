---
layout: post
title: Java Fast Track - Data Types
author: Tony Xu
category: Java
description: Summarized data types of Java in one table.
---
![gorge]({{ site.baseurl }}\img\columbiagorge.png)

The **primitive** types and **object reference** are two group types in Java. Boxed primitive types are object types but **immutable**.

Primitive|Boxed      |Description
---------|-----------|---------------
boolean  |Boolean    | true or false
byte     |Byte       | 8-bit signed, -2^7~2^7-1
short    |Short      | 16-bit signed, -2^15 to 2^15-1
char     |Char       | 16-bit Unicode
int      |Integer    | 32-bit signed, -2^31~2^31-1
long     |Long       | 64-bit signed, -2^63~2^63-1
float    |Float      | 32-bit floating point
double   |Double     | 64-bit floating point
char[]   |String     | N-byte Unicode string

Java supports "auto boxing". That means, Java can "box" a primitive type into its Boxed version or vive versa ("unbox").

## REFERENCE
1. Jakob Jenkov, [jenkov.com](http://tutorials.jenkov.com/java/index.html)
