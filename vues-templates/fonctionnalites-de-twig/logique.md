# Logique

### Syntaxe

La syntaxe est très proche de celle de PHP. Attention toutefois, les opérateurs de comparaison ne s'écrivent pas de manière identique. Le `&&` de PHP s'écrit `and` dans TWIG, et le `||` de PHP s'écrit `or` dans TWIG.

Les logiques sont définies entre ces balises <mark style="color:yellow;">**\{%**</mark>** ... **<mark style="color:yellow;">**%\}**</mark>.

### Tests

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

### Boucles

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
