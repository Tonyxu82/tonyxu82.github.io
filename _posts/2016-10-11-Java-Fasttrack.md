---
layout: post
title: JAVA FAST TRACK (In Progress)
author: Tony Xu
category: Java
---
![gorge]({{ site.baseurl }}\img\columbiagorge.png)

A programming language is like our second language. If you does not use it for a while, then it will disapear from our memory. The best way is to
practice it by writing code snippets everyday.


<!--description-->

## DATA TYPES

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

## FILES

In Java Programming Lanaguge, File operations relates to
[java.io.File](https://docs.oracle.com/javase/7/docs/api/java/io/File.html)
class.

### create

We can create a file by using
[createNewFile()](https://docs.oracle.com/javase/7/docs/api/java/io/File.html#createNewFile())
method.

```java
//Create a file by using createNewFile() method
public static void CreateFile(String fileName){
  try{
    File file = new File(fileName);
    if(file.createNewFile()){
      System.out.println("Success create "+fileName);
    }else{
      System.out.println("Failed create"+fileName);
    }
  }catch(IOException e){
    e.printStackTrace();
  }
}
```

### read



### update

### delete

If a file exists, we can use [delete()](https://docs.oracle.com/javase/7/docs/api/java/io/File.html#delete())
method to delete it.

```java
//Delete a exist file
public void DeleteFile(fileName){
  File file = new File(fileName);
  if(file.delete()){
    System.out.println("Success to delete the file!");
  }else{
    System.out.println("Fail to delete the file!");
  }
}
```

## NETWORKING

## CONCURRENCY

## REFERENCE

1. Tutorials Point, [Java Programming Examples](https://www.tutorialspoint.com/javaexamples/index.htm)
2. Joshua Bloch, [Effective Java 2nd](https://www.amazon.com/Effective-Java-2nd-Joshua-Bloch/dp/0321356683)
3. Jakob Jenkov, [jenkov.com](http://tutorials.jenkov.com/java/index.html)
