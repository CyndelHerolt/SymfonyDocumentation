---
description: Des filtres pour modeler les variables
---

# Filtres

TWIG propose un grand nombre de filtres permettant d'agir sur les variables. La liste complète est disponible [ici](https://twig.symfony.com/doc/3.x/).\
Vous trouverez dans cette liste de quoi, entre autres, formater, transformer et comparer vos données. Mais si vous ne trouvez pas qu'il vous faut, vous pouvez très bien créer vos propres filtres.

### Utiliser les filtres par défaut de TWIG

Afin d'appliquer un filtre à une variable appelée dans un template la syntaxe est la suivante :&#x20;

```twig
{{ variable|nomDuFiltre }}
```

Vous pouvez cumuler les filtres sur une seule et même variable à condition de les organiser dans le bon ordre :&#x20;

```twig
{{ variable|filtre1|filtre2|filtre3 }}
```

### Créer vos propres filtres

Afin de créer des filtres nous allons exploiter le concept d'[Extension Twig](https://twig.symfony.com/doc/3.x/advanced.html#creating-an-extension).

Pour ce faire, il faut créer une Class qui va étendre Twig\Extension\AbstractExtension. Cette Class peut être créée n'importe où dans le dossier src mais par soucis d'organisation vous pouvez la mettre dans le dossier src/Twig.

Dans cette Class, il faut créer une méthode qui permettra de définir les filtres à créer. Cette méthode doit retourner un tableau d'objets TwigFilter. Il faut également attribuer un nom à chaque filtre qui permettra de les appeler dans la Vue Twig et rédiger une méthode qui sera appelée lorsque le filtre sera utilisé.

Voici un exemple de filtre permettant de formater un nombre en ajoutant les symboles € ou $ :&#x20;

{% code overflow="wrap" %}
```php
<?php

namespace App\Twig;

use Twig\Extension\AbstractExtension;
use Twig\TwigFilter;

// La classe hérite de AbstractExtension afin d'exploiter le concepte d'Extension Twig
class AppExtension extends AbstractExtension
{
    public function getFilters()
    {
        // Retourne un tableau d'objet TwigFilter qui permet à Symfony de     l'identifier comme étant un filtre.
        return [
        // On passe en paramètre le nom qui nous permettra d'utiliser le filtre dans nos vue ('price') et le contenu filtré ($this) et la méthode qui va être appelée à l'usage du filtre ('formatPrice').
            new TwigFilter('price', [$this, 'formatPrice']),
        ];
    }
    
    // La méthode qui sera appelée à l'usage du filtre
    public function formatPrice($number, $symbol, $decimals = 0, $decPoint = '.', $thousandsSep = ',')
    {
        $price = number_format($number, $decimals, $decPoint, $thousandsSep);
  
        if ($symbol == '€') {
            $price = $price . ' €';
        }
        elseif ($symbol == '$') {
            $price = '$ '.$price;
        }

        return $price;
    }
}

```
{% endcode %}

Afin d'appliquer ce filtre dans une Vue Twig la syntaxe est la suivante :&#x20;

```twig
{{ 10|price('€', 2, ',', ' ') }}
{{ 10|price('$', 2, '.', ',') }}
```

Dans cet exemple notre filtre retourne simplement une variable et un caractère mais il est également possible de générer du HTML.

Dans ce cas, il sera nécessaire d'informer Symfony qu'il est autorisé à afficher le HTML passé dans le filtre. Par défaut l'utilisation d'un filtre incluant du code HTML renverrai une erreur car cette pratique peut engendrer des problèmes de sécurité.\
Pour autoriser Symfony à afficher le HTML, deux solutions sont envisageables.

#### Un filtre TWIG

Vous pouvez ajouter dans votre Vue le filtre `raw` déjà existant dans TWIG :&#x20;

{% code overflow="wrap" %}
```twig
{{ variable|votreFiltre|raw }}
```
{% endcode %}

#### Un paramètre dans l'objet TwigFilter

Si le filtre doit renvoyer du code HTML qui sera systématiquement affiché, il est possible de passer l'autorisation en paramètre de l'objet TwigFilter :&#x20;

{% code overflow="wrap" %}
```php
new TwigFilter('nomDuFiltre', [$this, 'laMethode'], ['is_safe' => ['html']])
```
{% endcode %}
