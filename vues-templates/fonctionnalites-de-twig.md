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

Un appel sous la forme __ `{{ foo['bar'] }}` est possible mais seulement si il s'agit d'un tableau PHP. Il vérifiera alors :&#x20;

1. Si `foo` est un tableau et `bar` un élément valide,
2. si non, il retourne une valeur null

### Logique

### Héritage et inclusion

### Filtres

### Assets



