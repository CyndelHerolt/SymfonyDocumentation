---
description: Gestion simplifiée des URL internes des imports média, fichiers css et js
---

# Assets

### La version "classique"

Symfony propose un bundle permettant une gestion simplifiée des imports média, fichiers css et js. L'ajout de ce bundle à un projet se fait de la manière suivante :&#x20;

```sh
composer require symfony/asset
```

Une fois ce bundle installé, il devient possible d'importer facilement des <mark style="color:yellow;">**assets**</mark> stockés dans le dossier public d'un projet. \
Pour l'utiliser dans une Vue Twig, la syntaxe est la suivante :&#x20;

```twig
{# importer une image stockée dans /public/images/ #}
<img src="{{ asset('images/logo.png') }}" alt="Symfony!" />

{# importer unfichier css stocké dans /public/css/ #}
<link href="{{ asset('css/blog.css') }}" rel="stylesheet" />
```

### Avec Webpack-Encore

Depuis la version 3.4 et 4, Symfony propose de gérer les assets avec [WebPack-Encore](../../bundles/webpack-encore.md).&#x20;

Une simple ligne de code permet alors de récupérer tous les assets à partir du moment où ils ont été importés dans le fichier app.js ou app.css.

{% code overflow="wrap" %}
```twig
{# templates/base.html.twig #}
<!DOCTYPE html>
<html>
    <head>
        <!-- ... -->

        {% raw %}
{% block stylesheets %}
            {# 'app' must match the first argument to addEntry() in webpack.config.js #}
            {{ encore_entry_link_tags('app') }}

            <!-- Renders a link tag (if your module requires any CSS)
                 <link rel="stylesheet" href="/build/app.css"> -->
        {% endblock %}

        {% block javascripts %}
            {{ encore_entry_script_tags('app') }}

            <!-- Renders app.js & a webpack runtime.js file
                <script src="/build/runtime.js" defer></script>
                <script src="/build/app.js" defer></script>
                See note below about the "defer" attribute -->
        {% endblock %}
{% endraw %}
    </head>

    <!-- ... -->
</html>
```
{% endcode %}

### Avec AssetMapper

{% hint style="warning" %}
AssetMapper n'est disponible qu'à partir de la version 7 de Symfony
{% endhint %}

