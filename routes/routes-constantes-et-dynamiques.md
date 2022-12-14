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

Dans l'exemple ci-dessus,&#x20;
