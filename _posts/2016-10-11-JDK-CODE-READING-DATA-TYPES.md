---
layout: post
title: JDK Code Reading - Data Types
author: Tony Xu
category: Java
description: Summarized data types of Java in one table.
---
![gorge]({{ site.baseurl }}\img\columbiagorge.png)

I have a dream to be a code guru someday. It is not only need to write code everyday and also need to read others code. So I start a self long term project to analyze JDK source code. The version of source code used to study is OpenJDK 8u40-b25. 

## Types in Java

There are two group types in Java
- Primitive
- Object

For each primitive type, Java also provides a boxed (object) types respectively for the [reasons](http://stackoverflow.com/questions/3579035/why-are-there-wrapper-classes-in-java)
- Treat a data with certain type generically/polymorphically as an Object.
- Use in collection
- Make null value possible

Java supports "auto boxing". That means, Java can "box"  primitive type into its Boxed version or vive versa ("unbox").

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

We need pay attention, all data of boxed type are **immutable**.


## Boolean
