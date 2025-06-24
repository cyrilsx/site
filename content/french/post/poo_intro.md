---
title: "Introduction à la POO"
date: 2025-06-23T11:05:05-05:00
tags: [dev, poo]
---
# Introduction à la POO

Il existe deux types de paradigme de programmation :
 1 - Impératif
 2 - Déclaratif

> Un paradigme de programmation est une manière (haut niveau) de concevoir et structurer des programmes informatiques.

Nous allons nous penché sur le côté impératif. Le plus populaire est la POO (Programmation Orienté Objet). 

## L'anatomie de l'objet caché par l'encapsulation

La base de la POO est l'objet qui représente une idée ou un objet physique. Par exemple, une _maison_ peut un objet. 

Un objet est composé de :
 - données qu'on appelle **attributs**
 - messages pour intéragir avec l'objet qu'on appelle des **méthodes**

Comme dans la vie réelle, les objets ont des relations entre eux et peuvent intéragir ensemble. 
Les objets ont un état interne : la structure est caché. Il est possible de modifier la structure de l'objet sans
impacté les objets qui l'utilisent. Ce concept s'appelle l'**encapsulation** et est un pilier de la POO.

## Les différents types de l'objet créé le polymorphisme

En POO, les objets sont typés. Un objet peut avoir plusieurs types : c'est le **polymorphisme** (second pilier de la POO).
C'est comme si un homme avait plusieurs dénominations : 
  - homme
  - être humain
  - vivant
Chacune de ces dénominations correspond à un objet `homme`.

Le type est généralement déclaré par une classe. En java, il est possible de déclarer un type avec les mots clé `class` et `interface`.

## L'abstraction pour des idées communes

L'**abstraction** est encore un des piliers de la POO. Il permet de rassembler des concepts de haut niveau. Ainsi, l'abstration est d'une grande aide pour la réutilisation de code.
Elle est aussi très utile pendant le développement pour définir des concepts et les utilisés sans se soucier de leurs implémentations.

Par exemple, notre application a besoin d'une communication entre un serveur et un client. Plutôt que passer du temps à développer la solution, il est possible de créer une abstraction et de l'utiliser par le 
reste du code.

## Héritage, le lien fort entre les objets

L'**héritage** est un partie intégrante du type et est considéré comme le 4e pilier de la POO. Il est lié au concept de type discuté ci-dessus. Il permet de créer des liens de parenté entre les objets. Il est utlisé pour réutiliser le code, ce qui
est correcte si le lien de parenté est justifié.
Certains langages permets un héritage plus ou moins étendu. 

Un exemple d'héritage peut être considéré chez les animaux. 
Un type `Animal` est un parent d'un type `Mamifère` qui lui même est un parent d'un type `Félin`.
On peut dire `Félin` est un enfant de `Mamifère`.

### Question
1- Tentez de trouver d'autres relations qui pourrait utiliser l'héritage ?
2- Selon, quelles sont les inconvénients à l'héritage ?

## Conclusion

Il existe une quantité incroyable de resource sur la POO. Cette petite introduction donne un aperçu des principaux concepts de la POO.


