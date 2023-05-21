---
description: Pour une gestion de modules simplifiée
---

# Webpack-Encore

### Quelle fonction pour Webpack-Encore ?

Webpack-Encore est un dérivé de [**Webpack**](https://webpack.js.org) (outil logiciel open-source de type « module bundler » (littéralement, « groupeur de modules ») spécialement conçu pour et par Symfony (même si il peut être utilisé dans n'importe quel application PHP et autres langages côté serveur).

L'utilisation de Webpack-Encore offre une gestion simplifiée des fichiers css/scss, js, images etc. Il va entre autres permettre de les regrouper dans le dossier public pour les rendre accessibles dans les Vues, de les minifier, de les compiler... Il permet également de faire usage des langages types VueJS, React etc.

### Installation

L'installation et l'utilisation de Webpack et donc de Webpack-Encore nécessite d'avoir installé [NodeJS](https://nodejs.org/en/) afin de disposer de [npm](https://www.npmjs.com/) ou [yarn](https://yarnpkg.com/) qui sont des gestionnaires de packages.&#x20;

{% hint style="info" %}
**npm ou yarn**

Il est préférable d'en choisir un et de se limiter à son unique utilisation pour un projet.
{% endhint %}

#### Installation de NodeJS et npm ou yarn

{% code overflow="wrap" %}
```sh
# met à jour la liste des sources de packages avec les dernières versions des packages dans les référentiels
sudo apt update

# installer nodeJS
sudo apt install nodejs

# vérifier si node est bien installé et voir la version
node -v

# installer npm
sudo apt install npm

    # ou
    
# installer yarn
sudo apt install yarn

# vérifier si npm ou yarn est bien installé et voir la version
npm -v

    #ou

yarn -v
```
{% endcode %}

#### Installation de Webpack-Encore

```bash
# installer et activer WebpackEncoreBundle
composer require webpack-encore-bundle

# installer les dépendances front
yarn install

    #ou

# installer les dépendances front
npm install
```

L'installation et la création de Webpack-Encore a engendré quelques nouveautés dans le projet :&#x20;

* La création du dossier `assets` qui contient tous les fichiers "front" du projet (SCSS, CSS, JS, images ...) dans leur version non compilée.
* L'ajout de `node_modules/` au fichier `.gitignore`.
* La création du fichier `package.json` qui contient les dépendances "front" du projet.
* La création du fichier `webpack.config.js` qui contient la configuration de Webpack et la liste de toutes les tâches qu'il doit réaliser.

Dans le dossier `assets`, plusieurs fichiers ont été initialisés :&#x20;

* <mark style="color:yellow;">`assets/app.js`</mark>
* `assets/bootstrap.js`
* `assets/controllers.json`
* `assets/styles/app.css`
* `assets/controllers/hello_controller.js`

Considérez le fichier <mark style="color:yellow;">`app.js`</mark> comme une application JavaScript autonome. C'est dans ce fichier qu'il faut importer toutes les <mark style="color:yellow;">dépendances JavaScript et CSS</mark> dont l'application a besoin, il s'occupera lui-même des différentes compilations. Tous les imports seront lus et compilés en un seul fichier final `app.js` et un seul fichier final `app.css`.

Les autres fichiers `bootstrap.js`, `controllers.json` et `hello_controller.js` sont liés à l'utilisation de [Stimulus et Symfony UX](https://symfony.com/doc/current/frontend/encore/simple-example.html#stimulus-symfony-ux).

{% hint style="warning" %}
Ces automatismes sont effectifs seulement si vous utilisez <mark style="color:yellow;">**Symfony Flex**</mark>, dont l'installation est automatique à la création d'un projet depuis Symfony4. Mais si vous utilisez une version antérieure et/ou que vous voulez l'ajouter à un projet existant [c'est par ici](https://symfony.com/doc/current/setup/flex.html) !
{% endhint %}

### Configuration

Toute la configuration de Webpack-Encore est définie dans le fichier <mark style="color:yellow;">`webpack.config.js`</mark> qui se trouve à la racine du projet. Il contient par défaut la configuration basique nécessaire à son fonctionnement.

```javascript
// webpack.config.js
const Encore = require('@symfony/webpack-encore');

Encore
    // directory where compiled assets will be stored
    .setOutputPath('public/build/')
    // public path used by the web server to access the output path
    .setPublicPath('/build')

    .addEntry('app', './assets/app.js')

    // uncomment this if you want use jQuery in the following example
    .autoProvidejQuery()
;

// ...
```

La partie clé est <mark style="color:yellow;">`addEntry()`</mark> : cela indique à Encore de charger le fichier assets/app.js et de suivre toutes les instructions `require()`. Il compilera ensuite tout ensemble et - grâce au premier argument `app` - créera les fichiers finaux `app.js` et `app.css` dans le répertoire `public/build`.

Afin d'utiliser les fichiers "front" d'un projet, il faut que Webpack-Encore <mark style="color:yellow;">génère les fichiers compilés</mark> dans le répertoire `public/build`. \
Pour ce faire, il existe la commande suivante :&#x20;

```sh
yarn dev
    #ou
npm run dev
```

Cette commande lance Webpack-Encore et va créer entre autres, un fichier `entrypoints.json` dans le répertoire public/build qui contiendra la liste des fichiers compilés et leurs chemins respectifs qui permettra ensuite à TWIG de les charger.

Lorsque vous apportez des modifications à la partie front d'une application, il devient nécessaire de relancer Webpack-Encore pour relancer la compilation des fichiers. Il existe une commande qui permet de surveiller les fichiers du répertoire assets et de <mark style="color:yellow;">relancer Webpack-Encore à chaque modification</mark> :&#x20;

```sh
yarn watch
    #ou
npm run watch
```

{% hint style="info" %}
Les commandes `dev` et `watch` sont des raccourcis définis dans le fichier `package.json`.
{% endhint %}

Lors du <mark style="color:yellow;">passage en production</mark>, il faut générer une nouvelle version des fichiers spécifique à ce processus. La commande est la suivante :&#x20;

```sh
yarn build
    # or
npm run build
```

{% hint style="danger" %}
Si vous apportez des modifications au fichier `webpack.config.js`, il est nécessaire de relancer Webpack-Encore pour que les modifications soient prises en compte.
{% endhint %}

### Requête des modules JavaScript

WIP

### Utilisation de SaSS/SCSS

WIP

###
