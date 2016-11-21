---
layout: post
title: Code Reading - java.lang.String
author: Tony Xu
category: Java
description: String class is used to represents character strings in Java. The strings of this class are immutable once they are created.
---

# INTRUCTION

String class is used to represents character strings in Java. The strings of this class are immutable once they are created.

# IMMUTABLENESS

Programcreek[1](http://www.programcreek.com/2013/04/why-string-is-immutable-in-java/) gives 5 reasons  for immutablesness of String in Java.
1. A immuatble object in object pool can be reused to avoid overhead of creating a new object.
2. The hashcode of a String object can be cached to avoid the overhead caused by computing hashcode.
3.

Internally, String class store the data in a char array.

```java
private final char value[];
```


# REFERENCE
1. [Why String is immutable in Java?](http://www.programcreek.com/2013/04/why-string-is-immutable-in-java/)
