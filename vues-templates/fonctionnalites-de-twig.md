# Fonctionnalités de TWIG

### Variables

Twig permet de manipuler des variables définies en PHP dans le Controller ou le Model.&#x20;

La syntaxe est la suivante :&#x20;

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

Le résultat serait exactement le même si à la place du tableau associatif il y avait un objet `$tab` (une instance de Class) ayant comme propriété `$param1`.&#x20;
