---
layout: post
title: JAVA FAST TRACK
author: Tony Xu
category: Java
---
![gorge]({{ site.baseurl }}\img\columbiagorge.png)

A programming language is like our second language. If you does not use it for
a while, then it will disapear from our memory. The best way is to
practice it by writing code snippets everyday.


<!--description-->

## FILES
---
In Java Programming Lanaguge, File operations relates to
[java.io.File](https://docs.oracle.com/javase/7/docs/api/java/io/File.html)
class.

### create

We can create a file by using
[createNewFile()](https://docs.oracle.com/javase/7/docs/api/java/io/File.html#createNewFile())
method. A code snippet shows how to create a file.

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

## NETWORKING
---

## CONCURRENCY
---

## REFERENCE
---
1. Tutorials Point, [Java Programming Examples](https://www.tutorialspoint.com/javaexamples/index.htm)
2. Joshua Bloch, [Effective Java 2nd](https://www.amazon.com/Effective-Java-2nd-Joshua-Bloch/dp/0321356683)
