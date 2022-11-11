---
description: Un framework MVC libre écrit en PHP
---

# Découverte de Symfony

### Qu'est ce qu'un Framework ?

Un framework est un **ensemble d'outils et de composants organisés conformément à un plan d'architecture et des patterns**, l'ensemble formant un « squelette » de programme proposant des fonctionnalités internes exploitables et modulables. \
Ce squelette est composé de bibliothèques, de moteurs, de la configuration du projet... \
Un framework peut être spécialisé, sur un langage particulier, une plateforme spécifique, un domaine particulier : **reporting** _(mettre en scène des données)_, **mapping** _(mettre en correspondance les champs de plusieurs bases de données)_, etc.&#x20;

Il est généralement construit sur une structure bien définie qui impose un cadre de travail (traduction littérale de l’anglais : _framework_) spécifique à chaque framework.

### Le framework Symfony

Symfony est donc un ensemble de composants PHP ainsi qu'un framework MVC libre écrit en PHP qui utilise un moteur de template : TWIG. \
Il est possible d'utiliser entre autres les composants suivants :

* **Asset** : c’est le module pour générer des URL et effectuer différentes versions de fichiers image, feuilles de style CSS et applications JavaScript.
* **ClassLoader** : ClassLoader veille à ce que les classes PHP soient téléchargées automatiquement.
* **Debug** : met des outils à disposition pour contrer les bugs dans le code PHP, pour détecter les erreurs et les analyser.
* **DependencyInjection** : permet de définir des standards pour la création d’objets pour le projet Web en question.
* **EventDispatcher** : ce sont des composants élémentaires permettant la communication entre les modules, sous forme d’événements.
* **Form** : comprend des outils avec lesquels la création de formulaires HTML réutilisables est simplifiée.
* **Templating** : outils visant à créer un système de templates.
* **Translation** : module pour l’internationalisation d’un projet. &#x20;
* **Validator** : confère la possibilité de valider les classes créées.
* **Yaml** : télécharge et stocke les fichiers _.yml_.

### Un framework Orienté Objet

Organisé selon le modèle de la Programmation Orientée Objet (POO), Symfony dispose de Class prédéfinies. Ces Class seront dérivées et étendues par héritage selon les besoins spécifiques à chaque logiciel qui utilise le framework.\
Elles peuvent être complétées en fonction de besoins spécifiques grace à la notion d'héritage de la POO : \
Créer de nouvelles Class héritières des Class prédéfinies permet d'exploiter toutes les fonctionnalités que met en place le framework en plus de celles créés spécialement pour l'application.

###
