---
description: >-
  La Vue - ou Template - est un fichier dans lequel le code HTML est organisé et
  restitué.
---

# Introduction

## <mark style="color:yellow;">TWIG</mark>

### Quelle fonction pour la Vue ?

Elle définit ce que l'utilisateur voit lorsqu'il accède à une page web gérée par l'application. Elle est généralement écrite en HTML mais peut également utiliser d'autres langages comme le XML ou le JSON.\
En exploitant les Controller et les Model, la Vue récupère les données nécessaires pour afficher la page Web et les incorpore au bon endroit dans le code HTML.

Dans Symfony la Vue - ou Template - est généré avec un moteur de rendu de template : <mark style="color:yellow;">**TWIG**</mark>.

{% hint style="info" %}
Un moteur de template permet de limiter les logiques complexes pour réaliser des templates simples à coder. Il intègre généralement des fonctionnalités qui sont récurrentes dans le développement "front" et qui permettent de simplifier le code à écrire.
{% endhint %}

### Conventions d'usage

La syntaxe Twig est basée sur trois constructions :&#x20;

* <mark style="color:yellow;">**\{{**</mark>** ... **<mark style="color:yellow;">**\}}**</mark> => permet d'afficher le contenu d'une variable <mark style="color:red;">( ou le résultat de l'évaluation d'une expression ??? )</mark>
* <mark style="color:yellow;">**\{%**</mark>** ... **<mark style="color:yellow;">**%\}**</mark> => permet d'éxecuter une logique (une condition ou une boucle).
* <mark style="color:yellow;">**{#**</mark> ... <mark style="color:yellow;">**#}**</mark> => permet d'ajouter des commentaires au Model (contrairement aux commentaires HTML, ces commentaires ne sont pas inclus dans la page rendue).
