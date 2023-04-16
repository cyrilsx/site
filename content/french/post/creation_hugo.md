---
title: "hugo bosses - création d'un blog"
date: 2023-04-10T21:05:05-05:00
tags: [dev, website]
---
# Hugo Bosses

Je sais, je sais, quel jeu de mots minable !  Alors bienvenue ici! Comme vous avez pu le constater, ce site a été créé avec l'aide d'[hugo.io](https://gohugo.io). Je pense que le premier billet de blog doit être sur le système qui se cache derrière votre présente lecture.

## Hugo

Hugo est un générateur de site web statique. Je suis personnellement passé par les étapes suivantes :
1. Je suis plus fort que tout le monde : je créé **mon propre site** en _php_ et puis en _python_.
2. J'ai la flemme et une vie : j'utilise une **solution tout prête** en php avec un wysiwyg : _wordpress_.
3. Je code et je code : pourquoi pas tout en **markdown ou asciidoc** comme sur _github_ : hello Hugo

### Pourquoi j'ai choisi Hugo ?

Il faut bien distinguer ce que nous allons comparer. J'ai senti qu'il fallait séparer cette section en deux : 

1. Présenter les avantages de inconvénients d'un génération de site statique
2. Présenter le choix d'Hugo par rapport à ces concurrents dans ce monde là.

#### Les générateurs de site statiques

Avec une solution maison, il est clair que cela convient uniquement si vous avez du plaisir à coder, maintenir une solution. Et encore, je pense qu'il serait plus utile et amusant de participer un projet opensource.

En ce qui concerne les solutions prêtes à emploi, j'ai principalement travaillé avec _wordpress_ mais je ne me considère pas comme un expert. 

Les CMS _(Content Management System)_ sont indispensables pour les personnes qui n'ont **aucune envie** ou tout simplement pas le temps de s'intéresser aux **joies du code**. En quelques cliques, il est **facile** de créer son site, allant d'un simple blog à des solutions plus complexes grace au système de plugin.

Un générateur de site statique ne va pas ouvrir un système aussi **complet et accessible** au non-codeur que _wordpress_ ou autres CMS.

Alors **pourquoi choisir la solution des générateurs de site statique ?**

Ce que j'aime, en tant que codeur, c'est la simplicité **d'écrire du code avec un langage accessible** (avec l'aide d'_asciidoc_ ou _markdown_) et le gérer comme du code source. La base de données peut être oubliée, juste des fichiers textes. 

A l'origine, ces solutions ont pour but de simplifier voire d'enlever toute gestion d'infrastruture et de simplifier l'hébergement. A titre d'illustation, la base de données et toute la gestion qui va avec disparait. 

Pour un développeur, je trouve ça très rassurant. Tous les repères sont retrouvés, nous sommes des petits poissons dans l'eau. Cela permet d'utiliser un SCM _(Source Control Management)_ qui fournit l'historique, une système d'authentification, revue de l'article... De plus, on a un **large choix d'outils pour éditer** son contenu : intellij, vscode, vim, github et tout ce qui lit du fichier texte. Rien que ça! 

Pour clore ce chapitre, les fichiers textes au format _markdown_ me rassurent car il est très de reprendre les fichiers et de générer les pages soit-même ou d'utiliser un autre générateur si la solution initiale ne convient plus. 


> **_NOTE:_** L'hébergement est un sujet commun à tous que je ne vais pas traiter ici.


#### Hugo vs Jekyll

Pour être honnête, je n'ai pas d'expérience réél avec _Jekyll_. Il est surement l'outil le plus populaire dans sa catégorie. A l'origine, il a été créé pour _"blogger"_.

J'ai choisi Hugo pour trois raisons :
1. **La rapidité** : c'est le champion ;
2. **Les formats** : il gère le markdown et le asciidoc ;
3. **Un seul binaire** : Hugo, c'est un binaire et pas d'étape d'installation avec du npm, pip ou gems.

Je pense qu'au niveau plugins, personnalisations, communautés et montés en compétence, les deux solutions sont similaires. Jekyll a un léger avantage de partout sauf pour les trois points cités ci-dessus. 

Finalement, les deux solutions sont très bien. Si vous réalisez un blog, vous avez fait un bon choix.

### Qu'est ce qui se passe sous le capôt ?

Sous le capot, Hugo contient une arborescence de fichier qui contient les sources et les templates de votre site. Avec l'aide du CLI (L'exécutable en ligne de commande), Hugo va générer votre site web.

### Comment démarrer ?

Hugo est écrit en `go`. Donc il faut savoir que `git` et `go` sont souvent utilisés pour travailler avec Hugo. Cela ne doit pas être une surprise !

Pour l'installation, vous pouvez télécharger le binaire [sous github](https://github.com/gohugoio/hugo/releases).

Sous linux, vous pouvez lancer un terminal et c'est parti : 

```
$ hugo new site quickstart
$ cd quickstart
```
Cette première étape permet de générer l'application de base. 

```
$ git init
$ git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke themes/ananke
$ echo "theme = 'ananke'" >> config.toml
```
Ensuite, il faut installer un thème. Dans cet exemple. il s'agit de _ananke_.
Comme vous pouvez le constater, `git` est utilisé pour installer le thème.

```
$ hugo server
```
Cette commande lance un serveur de développement qui vous permettera de voir le résultat.

```
$ hugo new posts/premier-billet.md
```
Enfin, cette commande va créer un fichier du premier billet de blog sous `content/posts`.
Il ne vous reste plus qu'à vous mettre au travail.

### En savoir plus

Comme tout, il faut commencer par la [documentation](https://gohugo.io/documentation/) d'Hugo.
J'ai aussi lu quelques articles de ce [blog](https://www.regisphilibert.com/tags/hugo/).

Je vous laisse découvrir tout ça et à très bientôt.
