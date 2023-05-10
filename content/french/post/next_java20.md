---
title: "Les futurs fonctionnalités après java 20"
date: 2023-05-09T21:05:05-05:00
tags: [dev, java, voxxeddays] 
---
# Java Next - From Amber to Loom, from Panama to Valhalla
Inpiré de la présentation de Nicolai PARLOG - [Site](https://nipafx.dev/)

Il existe quatre projets pour résoudre les problèmes de java et pour le faire évoluer : 

* Amber
* Loom
* Panama
* Valhalla

Nous allons les passer en revue un par un. Suivant le degré de maturité, on peut s' amuser à parier quand est-ce qu'une fonctionnalité d'un des projets sera intégrée dans la JDK.

## Amber

Le but d'Amber est d'explorer et d'intégrer des fonctionnalités qui pourrait améliorer la lisibilité et la productivité dans _java_. Le projet est maintenu par Brian Goetz (architecte oracle et auteur de _java concurrency_).

Amber est connu pour les fonctionnalités suivantes : 

* le mot clef `var`
* les `record`
* le `switch case`
* ...

Pour plus d'information, vous pouvez consulter leur [site](https://openjdk.org/projects/amber/).

### String Template

La _JEP 430_ permet d'intéger les _string_ ou les bloques de texte avec des expressions embarqués et des processeurs.
Qu'est ce que cela veut dire dans la pratique ?

#### Probème

La concaténation de _string_ avec la dernière version du jdk (_20_):

* **Concaténation** est difficile à lire
```java
String addition = x + " plus " + y + " equals " + (x + y);
System.out.println(addition);

#> 2 plus 3 equals 5
```

* Concaténation via **StringBuilder** est très verbeux
```java
 addition = new StringBuilder()
   .append(x)
   .append(" plus ")
   .append(y)
   .append(" equals ")
   .append(x + y)
   .toString();
System.out.println(addition);

#> 2 plus 3 equals 5
```

* Le **formatter** de _string_ n'est pas très lisible
```java
addition = String.format("%2$d plus %1$d equals %3$d", x, y, x + y);
System.out.println(addition); 

// ou
addition = "%2$d plus %1$d equals %3$d".formatted(x, y, x + y);
System.out.println(addition);

#> 2 plus 3 equals 5
```

* Le **message formatter** est boiler plate
```java
// Via le message formatter
MessageFormat mf = new MessageFormat("{0} plus {1} equals {2}");
addition = mf.format(new Integer[] {x, y, x + y});
System.out.println(addition);
```

#### Solution

La première solution étudiée est l'interpolation qui est populaire dans beaucoup d'autre langage.

```java
// Interpolation
// Python         f"{x} plus {y} equals {x + y}"
// Scala          s"$x plus $y equals ${x + y}"
```

Cependant, cette solution n'est pas retenu car elle permet des attaques de type SQLInjection, XML code injection...
Il faut faire mieux. Pourquoi pas _typer_ le contenu du texte avec l'injection de paramètre.

```java
var property = "Hello World";
var stringTemplate = STR. """
        Mon message \{property}
    """;
```


```java
var filtre= "user"";
var stringTemplate = SQL. """
        SELECT u.name, u.groups
        FROM user u 
        WHERE u.groups = \{filtre}
    """;
----

Le typage nous permet de gérer les caractères spéciaux et d'échappements _(escape)_. Mais pour une expression SQL, il serait mieux de retourner
un `Statement` comme ci-dessous : 

```java
Statement statement = SQL. """
         SELECT u.name, u.groups
         FROM user u
         WHERE u.groups = \{filtre}
     """;
----

*Template expression* est composée de :

* un template : le texte
* un processeur : SQL, FMT, STR...

`FMT` et `STR` sont des processeurs fournis par le jdk. Cependant, il est possible de définir ces propres processeurs.
Ci-dessous, l'interface qui ouvre l'accès à des processeurs utilisateurs.

```java
package java.lang;
public interface StringTemplate {
    @FunctionalInterface
    public interface Processor<R, E extends Throwable> {
        R process(StringTemplate st) throws E;
    }
}
```

Ci-dessous, deux exemples de processeur qu'il sera possible de créer :

1. Un processeur simple interpolation
2. Un processeur JSON

```java
StringTemplate.Processor<String, RuntimeException> INTER =
    StringTemplate.Processor.of(StringTemplate::interpolate);

String s = INTER."\{x} plus \{y} equals \{x + y}";
```

```java
class JSONException extends Exception {}

StringTemplate.Processor<JSONObject, JSONException> JSON_VALIDATE =
    (StringTemplate st) -> {
        String stripped = st.interpolate().strip();
        if (!stripped.startsWith("{") || !stripped.endsWith("}")) {
            throw new JSONException("Missing brace");
        }
        return new JSONObject(stripped);
    };

String name    = "Joan Smith";
String phone   = "555-123-4567";
String address = "1 Maple Drive, Anytown";

try {
    JSONObject doc = JSON_VALIDATE."""
        {
            "name":    "\{name}",
            "phone":   "\{phone}",
            "address": "\{address}"
        };
        """;
} catch (JSONException off_at_me) {
    throw off_at_me;
}
```


### Simplification du main

Le but est qu'un débutant n'a pas à savoir tout ce qui compose la méthode `main`.

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```


```java
class HelloWorld { 
    void main() { 
        System.out.println("Hello World");
    }
}
```

Plus d'information sur [Paving the on-ramp](https://openjdk.org/projects/amber/design-notes/on-ramp).

### Super This is relaxed

Le but est d'enlever la retriction d'appeler en premier `super()` et `this()`.



## Panama

*Panama* permet l'interconnection entre la JVM et le monde native de votre OS.

Panoma travaille sur deux modules : 

1. Vector API
2. Fonction et mémoire externe API

### Vector API

Le but est d'optimiser les opérations arithmétiques sur les vecteurs avec les instructions et les registres processeurs.
Du travail est déjà fait par la jvm, cependant, il est très simple de perdre une optimization et la rendre explicite permet de la garder.

### Fonction et mémoire externe API

Le but est de fournir une alternative plus facile, plus performante et plus sécurisé que JNI et sun.misc.Unsafe.

Il sera possible de mettre en mémoire hors de la heap, ce qui est critique pour les applications qui repose sur
Lucene, TensorFlow, Netty et Ignite.

Ci-dessous, un exemple complet tiré de la [jep-242 - API](https://openjdk.org/jeps/424) : 

```java
// 1. Find foreign function on the C library path
Linker linker = Linker.nativeLinker();
SymbolLookup stdlib = linker.defaultLookup();
MethodHandle radixSort = linker.downcallHandle(
                             stdlib.lookup("radixsort"), ...);
// 2. Allocate on-heap memory to store four strings
String[] javaStrings   = { "mouse", "cat", "dog", "car" };
// 3. Allocate off-heap memory to store four pointers
SegmentAllocator allocator = SegmentAllocator.implicitAllocator();
MemorySegment offHeap  = allocator.allocateArray(ValueLayout.ADDRESS, javaStrings.length);
// 4. Copy the strings from on-heap to off-heap
for (int i = 0; i < javaStrings.length; i++) {
    // Allocate a string off-heap, then store a pointer to it
    MemorySegment cString = allocator.allocateUtf8String(javaStrings[i]);
    offHeap.setAtIndex(ValueLayout.ADDRESS, i, cString);
}
// 5. Sort the off-heap data by calling the foreign function
radixSort.invoke(offHeap, javaStrings.length, MemoryAddress.NULL, '\0');
// 6. Copy the (reordered) strings from off-heap to on-heap
for (int i = 0; i < javaStrings.length; i++) {
    MemoryAddress cStringPtr = offHeap.getAtIndex(ValueLayout.ADDRESS, i);
    javaStrings[i] = cStringPtr.getUtf8String(0);
}
assert Arrays.equals(javaStrings, new String[] {"car", "cat", "dog", "mouse"});  // true
```


## Valhalla

Valhalla est un projet qui veut permettre de déclarer des structures primitives (values) et des classes (identities).
Les problèmes sont avec les identités : 

* plus de mémoire pour le headers
* la mutabilité
* les locks à gérer

Est-ce nécessaires que tout soit `identité` ? 
Non, les _values_ classes pourraient permettre : 

* de garantir l'immutabilité
* plus d'optimization

```java
value record Name(String first, String last) {
    public String full() {
        return "%s %s".formatted(first, last);
    }
}

identity record Node(String label, Node next) {
    public String list() {
        return label + (next == null) ? "" : ", " + next.list();
    }
}
```

## Loom

*Loom* peut actuellement être résumer en deux parties : 

1. `Virtual Thread` permet de décorréler les threads systèmes des threads java. Attention, les virtuals threads ne vont pas remplacer les `java.lang.Thread`.
2. La concurrence structurée ([Structured concurrency](https://openjdk.org/jeps/428)) est une approche pour la programmation _multithread_ qui préserve la lisibilité, maintenir et l'observalibité du code.

Voir la section suivante pour plus de détails sur les [threads](vhttps://openjdk.org/jeps/425) ou il est possible de consulter leur [wiki](https://wiki.openjdk.org/display/loom/Getting+started).
## Bonus

* [Les actualités des version de java et de la sécurité](https://seanjmullan.org/blog/)
* Les articles [states of](https://openjdk.org/projects/valhalla/design-notes/state-of-valhalla/01-background)
* [which jdk](https://whichjdk.com/)

