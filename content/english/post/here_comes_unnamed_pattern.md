---
title: "Time for unnamed pattern in java"
date: 2024-03-01T15:28:25+02:00
tags: [java, dev] 
---

Already as a preview in Java 21, **unnamed pattern** is finally released in Java 22. The new feature in java is just the continuation of the long term vision of the [amber](https://wiki.openjdk.org/display/amber/Main) project.
Maybe it's a good time to put it together.

In Java 14, jdk team integrated a better version of **instanceOf**. No need to declare and cast anymore.
```
if(animal instance Cat cat) {
  cat.maouh();
}
```

In Java 16, **record** type allows us to create an immutable data class. It's the end of _javabean_ and _boilerplate_ code. 
For example, to create a tuple: 

```java
record(String product, BigDecimal price) {}
```

Then a first version of a **pattern matching** was released and suddenly our switch _keyword_ can return a result:

```java
int nbChars = switch(word) {
  case "is" -> 2;
  case "not" -> 3;
  case "fun" -> 4;
}
```
 
