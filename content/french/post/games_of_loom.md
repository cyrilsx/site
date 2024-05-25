---
title: "Game of loom - Mario Fusco"
date: 2023-08-10T21:05:05-05:00
tags: [dev, website]
---

# Game of Loom: implementation patterns and performance implications playing with virtual threads
Mario FUSCO

Voici une présentation sur les *Virtual Thread* du projet _loom_ illustré à travers un projet https://github.com/ebarlas/game-of-life-csp[github] sur le https://fr.wikipedia.org/wiki/Jeu_de_la_vie[jeu de la vie].

[jeux de la vie](java/gosper-glider-gun.gif)
 
Les problèmes des thread natifs :

-   couteux, consommateur de mémoire
-   limité en nombre

Donc *loom* introduit les vthreads :

-   plus de relation 1 pour 1 avec les threads système
-   plus de thread OS bloqué/en suspens

TIP: Virtual Thread peuvent être connu sous plusieurs nom: filber, user
mode thread, coroutine…

.Comparaison \[cols=“3,3,3”,stripes=even\] \|=== \| \|Native Thread
\|Virtual Thread

\|Taille metadata \|2kb \|300b

\|Mémoire \|1Mb prealloué pour stack \|au fur-et-a-mesure

\|Temps contexte switch \|1-10ps \|quelques ns \<1ps \|===

WARNING: Ce n’est pas parce qu’on peut en créer des millions qu’il faut
le faire.

Le but est de pouvoir une application scalable sans payer avec plus de
complexité.

*Virtual Thread* sont excellents pour attendre.

Virtual Thread sont une sucre syntaxique pour le
https://www.reactivemanifesto.org/\[reactive programming\].

==== Problème possible avec les virtuals threads

-   Loom utilise le heap pour stocker les virtual threads
-   Les blocks synchronisé ne sont pas reconnu comme bloquant comme le
    thread virtuel et son sous jacents sont bloqués
-   VThread scheduler ne peut pas être intégré avec le ForkJoin pool
    schedule
-   VThread n’est pas pré-emptive
-   Massive contexte switch d’un nombre important de virtual thread peut
    potentiellement causé beaucoup d’erreur de cache (L1 & L2)
-   ThreadLocal est toujours fonctionnelle mais consomme beaucoup de
    mémoire

TIP: VThread sont deamon par défaut.

==== Conclusion

.Possible DefOps manual locations \* vThread ne sont pas plus rapide
\*\* Ils n’exécutent pas magiquement plus d’instruction par seconde \*\*
Ils sont très bon pour attendre (attention au pinning) \*\* Leur but est
de maximiser l’utilisation des resources externes et d’améliorer le
débit Quelles sont les rééls avantages des vThreads ?:: \*\* Ils sont
très bon pour les cas de traitements avec beaucoup d’IO



