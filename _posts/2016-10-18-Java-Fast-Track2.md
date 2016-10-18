---
layout: post
title: Java Fast Track - File
author: Tony Xu
category: Java
description: How to operate a file in Java.
---
![gorge]({{ site.baseurl }}\img\badger.png)

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

## REFERENCE

1. Tutorials Point, [Java Programming Examples](https://www.tutorialspoint.com/javaexamples/index.htm)
2. Joshua Bloch, [Effective Java 2nd](https://www.amazon.com/Effective-Java-2nd-Joshua-Bloch/dp/0321356683)
3. Jakob Jenkov, [jenkov.com](http://tutorials.jenkov.com/java/index.html)
