# Fonctionnalités de TWIG

### Variables

Twig permet de manipuler des variables définies en PHP dans le Controller ou le Model.&#x20;

#### Syntaxe

{% code overflow="wrap" %}
```twig
{# afficher le contenu d'une variable dans une balise de paragraphe #}
<p>{{ maVariable }}</p>
```
{% endcode %}

Cette syntaxe sera identique que la variable soit un simple objet, un objet avec des propriétés ou bien un tableau associatif.

Par exemple, considérons un tableau `$tab['param1']`, pour récupérer l'objet 'param1' il suffit d'appeler tour à tour les éléments qui composent la variable :&#x20;

```twig
{{ tab.param1 }}
```

Le résultat serait exactement le même si à la place du tableau associatif il y avait un objet `$tab` (une instance de Class) ayant comme propriété `$param1`. \
Si la propriété `$param1` était un tableau associatif avec une clé `key1` :&#x20;

```
{{ tab.param1.key1 }}
```

#### Procédure&#x20;

Considérons l'appel de la variable `{{ foo.bar }}`, Twig l'inspècte de la manière suivante :&#x20;

1. Vérifie si `foo` est un tableau et `bar` un élément valide.
2. si non, `foo` doit être un Objet, il vérifie alors&#x20;
   * si `bar` est une Propriété valide,
   * si non, si `bar` est une Methode valide (même si bar est le constructor utiliser \_\_construct() à la place),
   * si non, si `getBar` est une Methode valide,
   * si non, si `isBar` est une Methode valide,
   * si non, si `hasBar` est une Methode valide,
   * si non, il retourne une valeur null.

Un appel sous la forme `{{ foo['bar'] }}` est possible mais seulement si il s'agit d'un tableau PHP. Il vérifiera alors :&#x20;

1. Si `foo` est un tableau et `bar` un élément valide,
2. si non, il retourne une valeur null

### Logique

#### Syntaxe

La syntaxe est très proche de celle de PHP. Attention toutefois, les opérateurs de comparaison ne s'écrivent pas de manière identique. Le `&&` de PHP s'écrit `and` dans TWIG, et le `||` de PHP s'écrit `or` dans TWIG.

Les logiques sont définies entre ces balises <mark style="color:yellow;">**\{%**</mark>** ... **<mark style="color:yellow;">**%\}**</mark>.

#### Tests

Il est possible d'avoir autant de elseif que nécessaire et un seul bloc else.

{% code overflow="wrap" %}
```twig
    {# initialisation de la logique #}
{% raw %}
{% if condition1 and condition2 %}
...
{% else if condition %}
...
{% else %}
...
{% endif %}
{% endraw %}
    {# clotûre de la logique #}
```
{% endcode %}

#### Boucles

Dans TWIG la seule boucle exploitable est le `for` on peut dire qu'elle est l'équivalent du `foreach` en PHP.

{% code overflow="wrap" %}
```twig
    {# initialisation d'une boucle qui varie de 1 à 10 #}
{% raw %}
{% for i in 1..10 %}
...
{% endfor %}
{% endraw %}
    {# clotûre de la boucle #}
```
{% endcode %}



### Héritage et inclusion

Avec TWIG il est possible d'user du concept d'héritage ; cela permet d'éviter les répétitions de code et donc d'alléger notre projet. Le concept d'héritage de TWIG est sensiblement similaire à celui de PHP, on définit un template parent à partir duquel d'autres template peuvent s'étendre. Les templates enfants peuvent alors substituer des parties du template parent avec le code qui leur est propre.

Pour des applications relativement complexes, il est recommandé de suivre la logique suivante :&#x20;

* Le template `base.html.twig` va contenir les éléments essentiels à l'ensemble des templates de notre application. On y trouvera entre autres `head`, `header`, `body`, `footer`. Ces éléments seront définis dans ce qu'on appelle des `block`.

On appelle le template parent en utilisant la logique `extends` de la manière suivante :&#x20;

```twig
{% raw %}
{% extends 'nomDuTemplate.html.twig' %}
{% endraw %}
```

Dans le template parent, on va définir des `block`&#x20;

### Filtres

### Assets



