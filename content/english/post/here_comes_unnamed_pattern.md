---
title: "Time for unnamed pattern in java"
date: 2024-03-01T15:28:25+02:00
tags: [java, dev] 
---

Already as a preview in Java 21, **unnamed pattern** is finally released in Java 22. The new feature in java is just the continuation of the long term vision from the [amber](https://wiki.openjdk.org/display/amber/Main) project.
Maybe it's a good time to put it together and look back from Java 14.

In Java 14, jdk team integrated a better version of **instanceOf**. No need to declare and cast anymore.
```
if(animal instance Cat cat) {
  cat.maouh();
}
```

It's time to move on to Java 15. **Sealed classes or interfaces** can be use to add constraints such as:
- Every subclasses must explicitly extend the sealed classes
- The sealed type must declared all this subclasses with the keyword **permits** (not needed if subclasses are in the same file
- Every subclasses must be final

In Java 16, **record** type allows us to create an immutable data class. Guess what, their purpose is too hold data. It's the end of _javabean_ and _boilerplate_ code. 
For example, to create a tuple: 

```java
record ProductWithPrice(String product, BigDecimal price) {}
```

Then a first version of a **pattern matching** was released and our switch _keyword_ allows us to use the **enhanced instanceOf**:

```java
String value = switch(obj) {
  case Integer i -> String.format("int %d", i);
  case Long l -> String.format("long %d", l);
  case Object o -> String.format("obj %s", o.toString());
}
```

Also, sealed interface can upgrade our code to something more safe and more readable. Is it the end of the pattern visitor.

```java
sealed interface TaxRate permit EuTaxRate, UsTaxRate {}
record EuTaxRate extend TaxRate {}
record UsTaxRate extend TaxRate {}

BigDecimal tax = switch(obj) {
  case EuTaxRate eu -> eu.tax();
  case UsTaxRate us -> us.tax();
}
```

