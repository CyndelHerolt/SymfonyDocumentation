# Création d'une application

### Conditions nécessaires

{% hint style="danger" %}
**L'ensemble de ce document est rédigé dans le contexte d'une utilisation d'un système Linux.** \
Si vous voulez faire tourner Symfony sur Windows ou MacOS par l'intermédiaire de WAMP, XAMP ou MAMP je vous conseille plutôt d'installer [**WSL**](https://learn.microsoft.com/fr-fr/windows/wsl/install) (pour Windows) ou [**Multipass**](https://multipass.run) (pour MacOS) pour disposer d'un sous-système Linux dans lequel vous pourrez travailler plus simplement avec Symfony.

L'utilisation de [**Docker**](https://www.docker.com) est également une solution viable qui prend tout son intérêt si vous devez cumuler les projets Symfony. Cette option n'est pas documentée ici pour le moment mais vous pouvez trouver toutes les informations [ici](https://symfony.com/doc/current/setup/docker.html).
{% endhint %}

* Installer [Composer ](https://getcomposer.org/download/)
* Disposer de PHP 8.1 ou une version supérieure et ces extensions :  [Ctype](https://www.php.net/book.ctype), [iconv](https://www.php.net/book.iconv), [PCRE](https://www.php.net/book.pcre), [Session](https://www.php.net/book.session), [SimpleXML](https://www.php.net/book.simplexml), [Tokenizer ](https://www.php.net/book.tokenizer)  =>  (installables en utilisant Composer)
* Facultatif  =>  Installer Symfony CLI qui permet d'utiliser la commande `symfony` qui fournit tous les outils nécessaires au développement d'un projet en local. Une fois Symfony CLI installé, vous pouvez vérifier que vous avez rempli toutes les conditions en utilisant cette commande :&#x20;

<pre><code><strong>symfony check:requirements
</strong></code></pre>

### Création d'une application Symfony

Dans le command prompt, placez vous dans le dossier où vous souhaitez créer votre nouveau projet et lancer cette/ces commande/s :&#x20;

#### Avec Symfony CLI

<pre><code># Si vous construisez une application web standard => + de packages
<strong>symfony new my_project_directory --version="6.1.*" --webapp
</strong>
# Si vous construisez un microservice, une API ... => - de packages
<strong>symfony new my_project_directory --version="6.1.*"
</strong></code></pre>

#### Avec Composer

<pre><code># Si vous construisez une application web standard => + de packages
<strong>composer create-project symfony/skeleton:"6.1.*" my_project_directory
</strong><strong>cd my_project_directory
</strong><strong>composer require webapp
</strong>
# Si vous construisez un microservice, une API ... => - de packages
<strong>composer create-project symfony/skeleton:"6.1.*" my_project_directory
</strong></code></pre>

_la commande va créer un dossier contenant les fichiers nécessaires au fonctionnement de symfony, c'est dans ce dossier que vous travaillerez. Vous pouvez donc par exemple l'executer dans le dossier /var/www/html et vous obtiendrez /var/www/html/le\_projet._&#x20;

### Travailler sur une application Symfony déjà existante

Si vous devez travailler sur une application Symfony créée par d'autres développeurs, vous devez simplement récupérer les fichiers du projet et installer les différentes dépendance en utilisant Composer.

Partons du principe que vous récupérez un projet sur GitHub et que vos projets se trouvent dans le dossier `/var/www/html`, installez le projet en utilisant les commandes suivantes :&#x20;

<pre><code># cloner le projet et récupérer les fichiers (exemple /var/www/html)
<strong>cd /var/www/html
</strong><strong>git clone ...
</strong>
# installer les dépendances dans /vendor
<strong>cd my-project/
</strong><strong>composer install
</strong></code></pre>

Vous devrez probablement modifier le fichier .env afin d'y spécifier vos informations.

Afin d'identifier les changements nécessaires, vous pouvez accéder aux informations du projet en utilisant cette commande :&#x20;

<pre><code><strong>php bin/console about
</strong></code></pre>

### Lancer l'application

Si vous avez installé Symfony CLI vous avez accès au serveur interne de Symfony (à n'utiliser qu'en dev, jamais en prod), que vous pouvez utiliser grace à ces commandes :&#x20;

<pre><code># lancer le serveur
<strong>symfony server:start
</strong>
# lancer le serveur en tâche de fond
<strong>symfony server:start -d
</strong>
# arrêter le serveur
<strong>symfony server:stop
</strong></code></pre>

Une fois le serveur en marche, le command prompt vous retournera l'adresse grace à laquelle vous pouvez accéder au rendu de votre projet :&#x20;

<pre><code>[OK] Web server listening
      The Web server is using PHP CLI 8.1.2
<strong>      https://127.0.0.1:8000
</strong></code></pre>

Ouvrez votre navigateur et allez à l'adresse `http://localhost:8000/` . Si tout fonctionne, vous accédez à une page d'accueil.

Et voila, votre application Symfony est fonctionnelle !

{% hint style="info" %}
Vous pouvez utiliser le serveur avec n'importe quelle application PHP, pas seulement les projets Symfony.
{% endhint %}
