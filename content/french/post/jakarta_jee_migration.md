---
title: "Migrate package jakarta.* et javax.*"
date: 2024-01-12T11:05:05-05:00
tags: [java] 
---
# Migrate package jakarta.* et javax.*

## Avec l'outil fourni par Eclipse 

Avec la mise à jour vers spring boot 3, vous allez devoir mettre à jour tous vos packages provenant de JEE (jaxb, jpa...). 
Pendant cette migration, je me suis intéressé à la gestion des 2 packages de manière automatique de QueryDSL. En effet, avec QueryDSL, il est possible de choisir entre jakarta ou l'ancien nommage de package JEE. 
Pour cela, il utilise l'outil [Eclipse Transformer](https://github.com/eclipse/transformer) . Eclipse Transformer fournit des outils et des composants pour le runtime qui transforment les binaires Java, tels que les fichiers de classe, les JARs et WARs complets, en faisant correspondre les modifications aux paquets Java, aux noms de type et de ressources associé (traduction de la description du projet).

Par exemple, QueryDSL utilise le plugin org.eclipse.transformer.maven`  pour automatiquement créer le livrable jakarta sans devoir gérer une double version. Un exemple de pom est disponible sous github : [querydsl/querydsl-jpa-codegen/pom.xml](https://github.com/querydsl/querydsl/blob/master/querydsl-jpa-codegen/pom.xml).

*Extrait de code :*
```
    <plugin>
        <groupId>org.eclipse.transformer</groupId>
        <artifactId>org.eclipse.transformer.maven</artifactId>
        <version>0.2.0</version>
        <executions>
          <execution>
            <id>jakarta-ee</id>
            <goals>
              <goal>run</goal>
            </goals>
            <phase>package</phase>
            <configuration>
              <classifier>jakarta</classifier>
            </configuration>
          </execution>
        </executions>
      </plugin>
```

## Avec Intellij
Pour des cas plus simple, il est possible d'utiliser l'outil inclus dans Intellij : [IntelliJ IDEA's migration tool](https://www.jetbrains.com/guide/java/tutorials/migrating-javax-jakarta/use-migration-tool/).
