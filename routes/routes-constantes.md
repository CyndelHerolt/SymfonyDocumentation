# Routes constantes et dynamiques

### Routes constantes

Une Route constante est une Route dont l'URL ne change pas. Elle mène toujours à la même Vue ou à la même Methode de Controller.

En général, il est recommandé d'utiliser des routes constantes pour les pages statiques de votre site web, comme la page d'accueil ou la page "À propos", tandis que les routes dynamiques sont plus adaptées pour afficher des données qui changent en fonction des données passées à la route.

```php
#[Route('/monURL', name:'nom_de_la_Route')]
public function nomFonction(): Response
{
}
```

### Routes dynamiques

Une Route dynamique est une Route dont l'URL peut changer en fonction des données qui lui sont passées.&#x20;

```php
#[Route('/monURL/{id}', name:'nom_de_la_Route')]
public function nomFonction($id): Response
{
    echo $id;
}
```

Dans l'exemple ci-dessus, 'id' entouré de { } est une variable dynamique qui accèpte tous les caractères alphanumériques. \
Par exemple `/monURL/123` , `/monURL/456` sont deux URL différentes qui enclencheront lors de leur Request, la Méthode de Class à laquelle `/monURL/{id}` est liée.

Cette variable peut être exploitée dans le Controller, il suffit de déclarer en tant que paramètre de la Methode une variable avec le même nom que la variable d'url.\
Ici on affichera simplement le contenu de la variable.

Il est possible de cumuler plusieurs variables d'URL.

{% code overflow="wrap" %}
```php
#[Route('/monURL/{id}/{prenom}', name:'nom_de_la_Route')]
public function nomFonction($id, $prenom)
{
    echo $id.' '.$prenom;
}
```
{% endcode %}

On pourrait utiliser un autre séparation que le slash, comme par exemple <mark style="color:yellow;">-</mark>, <mark style="color:yellow;">.</mark> ou <mark style="color:yellow;">\_</mark>. La seule condition étant que Symfony puisse être en mesure de différencier les paramètres.
