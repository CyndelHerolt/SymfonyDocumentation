---
description: >-
  Récuperer et manipuler des éléments provenance de la requête HTTP du client
  (utilisateur et/ou navigateur)
---

# Manipulation des Requêtes

### Méthode de traitement des requêtes par Symfony

* L'utilisateur demande une **Ressource** au navigateur
* Ce dernier envoie une <mark style="color:yellow;">**Requête**</mark> au serveur
* Symfony execute l'objet <mark style="color:yellow;">**Request**</mark> en question dans l'application
* L'application récupère l'objet **Response** généré par l'execution de l'objet <mark style="color:yellow;">**Request**</mark>
* Le serveur envoie la **Response** au navigateur
* Le navigateur partage la **Ressource** à l'utilisateur



La manipulation des Requêtes requiert le passage en paramètre d'une Méthode, un Objet de type Request. _Cette façon de faire est appelée une **injection de dépendance**._ \
Il faut alors importer la [Class Request](https://github.com/symfony/symfony/blob/6.1/src/Symfony/Component/HttpFoundation/Request.php) native de Symfony qui permet d'exploiter les requêtes en ajoutant cette ligne :&#x20;

```php
use Symfony\Component\HttpFoundation\Request;
```

Ensuite, pour passer le paramètre à la Méthode la syntaxe est la suivante :&#x20;

```php
public function nomFonction(Request $request)
{ 
    ...
}
```

On peut alors exploiter la Requête en utilisant la variable <mark style="color:blue;">`$request`</mark> de cette manière :&#x20;

{% code overflow="wrap" %}
```php
public function nomFonction(Request $request)
{ 
//Données injectées dans un formulaire où le formulaire a été créé dans le     Controller grace à l'instruction : $form=$this>createForm( ... );
    $form->handleRequest($request);
    
//Données injectées dans un input de formulaire dans une vue
    $request->request->get('inputName');

//Ajax request
    $request->isXmlHttpRequest();

    $request->getPreferredLanguage(array('en', 'fr'));

//GET & POST variables
    $request->query->get('page');
    $request->request->get('page');

//SERVER variables 
    $request->server->get('HTTP_HOST');

//instance of UploadedFile identified by foo
    $request->files->get('foo');

//COOKIE value
    $request->cookies->get('PHPSESSID');

//HTTP request header, with normalized, lowercase keys
    $request->headers->get('host');
    $request->headers->get('content_type');
}
}
```
{% endcode %}

### Les Requêtes dans les Routes

Les [routes dynamiques](broken-reference) permettent de générer des requêtes en passant par l'URL. Pour exploiter ce type de Requête dans le Controller, il suffit d'initialiser la variable dans la route  et de la passer comme paramètre de la fonction. On peut ensuite agir sur cette variable et la récupérer dans le return. Cela permet l'écriture d'un code dynamique, modulé en fonction de l'information passée par l'URL.

Exemple : Moduler le titre <mark style="color:blue;">`<h1>`</mark> d'une page en fonction de l'URL

{% code overflow="wrap" %}
```php
// /src/Controller/ColorController
Class ColorController extends AbstractController {
//on passe le paramètre color à la route
    #[Route('/color/{color}', name: 'app_color')]
//on passe le paramètre color à la fonction
        public function colorBlue($color): Response
        {
//on retourne la vue 'color.html.twig' dans laquelle on pourra appeler la variable $color sous cette forme: {{ colorTitre }}
        return $this->render('color.html.twig', [
            'colorTitre' => $color;
        ]);
    }
}
```
{% endcode %}

```php
// /templates/color.html.twig
{% raw %}
{% extends 'base.html.twig' %}
{% block body %}
//on récupère la variable $color
        <h1>{{ colorTitre }}</h1>
{% endblock %}
{% endraw %}
```

Résultat : Si l'on accède à l'URL <mark style="color:blue;">`/color/blue`</mark>, le titre de la page sera "blue". (on pourrait également appeler la variable $color dans un bloc de style afin que le titre soit d'une couleur équivalente à la variable $color.

