---
title: "Developer Joy"
date: 2023-04-18T21:05:05-05:00
tags: [devops] 
---
# Developer Joy - How great teams get s%*t done
Sven PETERS - [Site internet](https://svenpet.com/)

Sven travaille chez Atlassian et est particulièrement interessé par le côté culture, productivité et management.
Après un exemple sur le Bethlehem Steel, il pose la question suivante : comment mesurer la productivité d'un développeur ?

* Nombre de LOC
* Nombre de tickets traités
* Les story points
* Les tailles de T-Shirt
* La fréquence des déploiements
* La période d'un cycle de développeur
* ....

En parallèle de la mesure de la productivité, qu'est ce qui est apparut dans leur monde en une dizaine d'année :

![Charge Cognitive](../post/voxxed2023/gen/developer_load.svg)

**Comment continuer à apprécier (et continuer à être productif) ce travail de développeur avec toute cette charge qui ne cesse d'augmenté ?**

Le métier de Dev est l'un des meilleures métiers au monde suivant _Sven_, mais ça commence à faire beaucoup. L'expérience 
du développement n'est plus la même. Comment un développeur peut avoir de la **joie** dans son art :

1. La qualité de développement
2. La progression de son développement 
[comment]: <> (Quelles sont les émotions lorsqu'on a l'impression que ça n'avance pas, qu'on est bloqué ? C'est terrible...)
3. La valeur qu'il apporte au monde (utilisateur, client, assuré, citoyen...)
[comment]: <> (On doit avouer, on se sent bien lorsqu'on sait que notre travail a du sens, qu'il apporte de la valeur)

## La qualité du `dev`

Commençons par la **dette technique**, en chiffre, c'est **42%** du temps de développement & seulement **10%** des équipes qui la gèrent.

### Coding guideline

Il faut avoir les outils pour automatiser la vérification de nos `coding guidelines` : plugins des éditeurs, sonar...

C'est bien, mais pas suffisant ;-)

### Revue de code

> **_NOTE:_**: Ne pas être un c*%@!? _antipathique_

La personne qui revoit le code devrait:

* Assumer que l'auteur du code est compétant
* Etre constructif sans ces remarques
* Expliquer son raisonnement

### Passer de bien à excellent
#### DORA 

Les métriques https://www.devops-research.com/research.html[DORA] et les indicateurs de flux permettent de **mesurer la performance des équipes responsables des produits.**

L’acronyme DORA signifie "The DevOps Research and Assessment Team". C'est une équipe de recherche de _Google_ qui a analysé
les pratiques Devops pendant 7 ans et a pu identifier les quatres paramètres clés pour mesurer les performances sur la pipeline
développement - livraison.


| Métrique  | Description | 
| :---      | :----       |
| Fréquence de déploiement _Deployment Frequency_ | La fréquence des mises en production réussies |
| Délai d'éxécution des `changes` _Lead time for changes_ | Temps entre la reception de la demande et son passage à un état déployable |
| Moyenne des temps de récupération _Mean Time to recover_ | Le temps entre une interruption due à une changement et à une défaillance du système et son rétablissement complet |
| Taux d'échec des changements _Change Failure Rate_ | La fréquence avec laquelle les changements qui entrainent des défaillantes ou des pannes après leur déploiement |


Une fois que ces métriques sont disponibles, il faut mettre en place *des baselines* _non-négociable_.

#### Check Ops _rituel hebdo_

Ce rituel peut être implémenté pour mieux comprendre et améliorer la santé opérationnelle des composants d'une équipe.
Elle consiste à poser les données/métriques (ex DORA) et suivre les améliorations dans le temps.

Les qualités des métriques suivantes à contrôler avec les baselines et le checkops:

* Résolution de bugs
* Taux d'échec des changements
* Temps pour rétablir une situation dégradée
* Temps de résolution des vulnérabilités
* Nombre d'occurence des incidents

#### La progression

Cette section commence avec quelques questions :

* Qui a participé au réunion d'avancement ces 2 dernières semaines ? (rétro, fin de spring pour la cdc)
* Qui a appricié ces réunions ?
* Qui a été interrompu pendant qu'il était entrain de coder ?

####  Flux de travail - les revues de code
![Flux de travail](../post/voxxed2023/gen/developer_flow.svg)

WARNING: Les revues de code prennent 3 jours en moyenne, soit 3 jours à travailler sur autres choses et revenir dessus.

Le conseil donné a été d'intégré un bot qui rappelle régulièrement qu'une pull request est en attente. Cela a permet dans le cadre d'une entreprise de passer de 3 à 1.2 jours pour
les pull request.

#### Flux de travail - l'autonomie

Un parallèle peut être considéré entre notre flux de travail et le [traffic routier](https://www.youtube.com/watch?v=yITr127KZtQ).

![Exemple du traffix routier](../post/voxxed2023/gen/traffic_flow.png)

Pour un flux de travail optimisé, une équipe doit être :

1. Autonome : dépendre au minimum des autres équipes - aspect organisationel/processus
2. Alignée _fortement_ : les membres partagent la même vision, les mêmes objectifs, la même compréhension...

#### Golden path - Paved Road

Les solutions logicielles créées durent longtemps dans le temps. Plus que ce que nous voudrions! Il faut donc assumer nos décisions dans le temps.

* Comment encourager l'innovation ? 
* Comment encourager l'adoption d'un outils ? 
* Comment laisser la liberté et garder une cohérance technique ?

![Golden Path spotify](../post/voxxed2023/gen/golden_path.png)

Ci-dessous le détail de ces concepts : 

* Spotify [golden path](https://engineering.atspotify.com/2020/08/how-we-use-golden-paths-to-solve-fragmentation-in-our-software-ecosystem/)
* Netflix [paved road](https://www.infoq.com/news/2017/06/paved-paas-netflix/)


#### La valeur du développement

Les développeurs doivent avoir du recul sur leur produit et avoir la vision globale. Ce n'est pas seulement créer, c'est aussi :

1. Wonder - Une phase de questionnement du problème
2. Explore - Une phase d'exploration des solutions
3. Make - Création d'une solution
4. Impact - Mesure l'impact de notre travail

Cela peut être lié au phase d'un projet :

1. Wonder -> Kick off d'un projet
2. Explore -> Prototypes
3. Make -> Demo
4. Impact -> mesurer, revoir les buts du projet

Les principes des demos : 

* Tous le monde est invité
* Montre la valeur aux clients/patenaires
* Permet de challenger la solution
* Célébrer et reconnaitre le travail

Utiliser la méthode [OKR](https://en.wikipedia.org/wiki/OKR) (Objective Key Result) : _I will (Objective) as measured by (Key Results)_. 

> **_NOTE:_**: Exemple, Je vais corriger ce bug pour que la majorité des utilisateurs mesurée par 7/10 puissent atteindre le service avec 1 sec de temps de réponse et 1% de taux d'erreur.

### Conclusion

Voici les points clés : 

* Si tu ne peux mesurer quelques choses, tu ne peux pas l'améliorer
* Mesurer ce qui est important, mais ne pas rendre important ce qu'on peut mesurer
* Demander l'avis aux développeurs / membres de l'équipe

Comment mesure la joie d'une developpeur :

* La rapidité de déployer de la qualité
* Temps d'attente
* L'indépendance d'exécution
* L'accès aux pratiques et aux outils
* L'effort de gestion des standards externes
* Gestion du code, de l'infrastucture et des pipelines
* Temps de monter en puissance
* Satistaction du developpeur

Si besoin, un [formulaire](https://srws7xs87wl.typeform.com/to/aVALqEZi) est disponible pour tous les curieux/curieuses.

### Mon avis

Le présentateur était très dynamique et très agréable à écouter. Il a donné beaucoup d'information. Il reste plus qu'à creuser et à débattre.




