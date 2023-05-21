---
description: >-
  Avec TWIG il est possible d'user du concept d'héritage ; cela permet d'éviter
  les répétitions de code et donc d'alléger notre projet
---

# Héritage et inclusion

### Héritage

Le concept d'héritage de TWIG est sensiblement similaire à celui de PHP, on définit un template parent à partir duquel d'autres template peuvent s'étendre. Les templates enfants peuvent alors substituer des parties des templates parents avec le code qui leur est propre.

Pour des applications relativement complexes, il est recommandé de suivre la logique suivante :&#x20;

* Le template `base.html.twig` va contenir les éléments essentiels à l'ensemble des templates de notre application. On y trouvera entre autres `head`, `header`, `body`, `footer`. Ces éléments seront définis dans ce qu'on appelle des <mark style="color:yellow;">**`block`**</mark>.

Le template `base.html.twig` pourrait par exemple ressembler à ça :&#x20;

{% code overflow="wrap" %}
```twig
{# templates/base.html.twig #}

<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>{% raw %}
{% block title %}Welcome!{% endblock %}</title>
        
    {% block stylesheets %}
        <link rel="stylesheet" type="text/css" href="/css/base.css"/>
    {% endblock %}
</head>
<body>
    <header>
        {% block header %}
            <nav>
                <ul>
                    <li><a href="#">menu item1</a></li>
                    <li><a href="#">menu item2</a></li>
                    <li><a href="#">menu item3</a></li>
                </ul>
            </nav>
        {% endblock %}
    </header>

    {% block body %}
    {% endblock %}

    <footer>
        {% block footer %}
                <ul>
                    <li>footer item1</li>
                    <li>footer item2</li>
                    <li>footer item3</li>
                </ul>
        {% endblock %}    
    </footer>

    {% block javascripts %}
        <script src="main.js"></script>
    {% endblock %}
{% endraw %}
</body>
</html>
```
{% endcode %}

<mark style="color:yellow;">**Les block tag de TWIG définissent les sections qui peuvent être substituer dans les templates enfants.**</mark> Ils peuvent être vides comme c'est le cas ici avec le `{% block body %}`, ou bien renfermer du contenu qui sera affiché si les templates enfants ne les remplacent pas.

{% hint style="info" %}
Le nom des block n'est pas imposé mais il est préférable de les nommer de manière logique. Pour vous retrouver plus facilement, il est possible de rappeler le nom d'un block dans le \{% endblock %\}.\
<mark style="color:blue;">\{% block body %\} \{% endblock body %\}</mark>
{% endhint %}

* On peut donc ensuite créer des templates qui hériteront de base.html.twig de la manière suivante :&#x20;

{% code overflow="wrap" %}
```twig
{# templates/blog/layout.html.twig #}

{% raw %}
{% extends 'base.html.twig' %}

{% block body %}
    <h1>Blog</h1>
    {% block page_contents %}{% endblock %}
{% endblock %}
{% endraw %}
```
{% endcode %}

Ici le contenu ajouté dans le `{% block body %}` vient alimenter le `{% block body %}` du template `base.html.twig`.&#x20;

* On pourrait même créer un autre template qui hériterait de celui-ci et qui viendrait alimenter le `{% block page_contents %}`. On pourrait d'ailleurs y définir du contenu venant remplacer les blocks définis dans le template base.html.twig.

{% code overflow="wrap" %}
```twig
{# templates/blog/index.html.twig #}

{% raw %}
{% extends 'blog/layout.html.twig' %}

{% block title %}Blog Index{% endblock %}

{% block header %}
            <nav>
                <ul>
                    <li><a href="#">menu item1</a></li>
                    <li><a href="#">menu item2</a></li>
                    <li><a href="#">menu item3</a></li>
                    <li><a href="#">Un nouvel item :)</a></li>
                </ul>
            </nav>
        {% endblock %}

{% block page_contents %}
    <ul>
        <li>Du contenu !</li>
    </ul>
{% endblock %}
{% endraw %}
```
{% endcode %}

Lorsque vous allez afficher la page index.html.twig, Symfony utilisera les trois templates liés par l'héritage pour créer le contenu final de la page.&#x20;

{% hint style="danger" %}
Si vous utilisez `extends`, il est impossible d'intégrer du contenu en dehors des block dans un template enfant.
{% endhint %}

### Inclusion

Dans le but de ne jamais répéter un code identique dans plusieurs fichiers on peut aussi simplement inclure des templates dans d'autres templates. \
Par exemple on pourrait créer une Vue qui contiendrait le contenu que l'on souhaite afficher dans le `{% block page_contents %}` créé plus haut et l'injecter dans le template `index.html.twig` :&#x20;

{% code overflow="wrap" %}
```twig
{# templates/blog/index.html.twig #}

{% raw %}
{% extends 'blog/layout.html.twig' %}

{% block title %}Blog Index{% endblock %}

{% block header %}
            <nav>
                <ul>
                    <li><a href="#">menu item1</a></li>
                    <li><a href="#">menu item2</a></li>
                    <li><a href="#">menu item3</a></li>
                    <li><a href="#">Un nouvel item :)</a></li>
                </ul>
            </nav>
        {% endblock %}

{% block page_contents %}
    {% include "_content.html.twig" %}
{% endblock %}
{% endraw %}
```
{% endcode %}

{% hint style="info" %}
on ajoute un underscore devant le nom de la vue lorsqu'on la créée pour signaler que ce n'est qu'un snippet
{% endhint %}
