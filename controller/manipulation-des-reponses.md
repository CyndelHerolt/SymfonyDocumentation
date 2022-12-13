---
description: >-
  Un objet Response contient toutes les informations d'une certaine Request qui
  doivent être renvoyées au client.
---

# Manipulation des Reponses

### Méthode de traitement des reponses par Symfony

* L'utilisateur demande une **Ressource** au navigateur
* Ce dernier envoie une **Requête** au serveur
* Symfony execute l'objet **Request** en question dans l'application
* L'application récupère l'objet <mark style="color:yellow;">**Response**</mark> généré par l'execution de l'objet **Request**
* Le serveur envoie la <mark style="color:yellow;">**Response**</mark> au navigateur
* Le navigateur partage la **Ressource** à l'utilisateur

La Response est l'objet fondamental pour Symfony. Un controller doit systématiquement retourner un objet Response.

Il existe plusieurs types de Response => JsonResponse, RedirectResponse, HttpResponse, BinaryFileResponse...\
La plus utilisée est Response.\
Afin de l'exploiter, il est nécessaire d'intégrer la [Class Response](https://github.com/symfony/symfony/blob/6.1/src/Symfony/Component/HttpFoundation/Response.php) native de Symfony qui permet d'exploiter les requêtes en ajoutant cette ligne :&#x20;

```php
use Symfony\Component\HttpFoundation\Response;
```

Ensuite, si l'on veut manipuler la Response à l'aide d'une méthode, on doit la récupérer dans le return ; ici ce code permet simplement d'afficher 'Ma response' qui est une chaine de caractère injectée manuellement en tant que contenu de la Response : \
_Dans l'état cette réponse n'est pas du HTML car rien n'est précisé dans ce sens dans le return._&#x20;

{% code overflow="wrap" %}
```php
//Ajout du type Response à la fonction
public function nomFonction(): Response 
{
    //On initialise la chaine de caractères 'Ma Response' comme contenu de l'objet Response
    return new Response('Ma Response');
}
```
{% endcode %}

Il est possible de retourner toutes sortes de données dans la Response (JSON, array, string, variables...).&#x20;

Dans l'exemple ci-dessous, on retourne une méthode [<mark style="color:purple;">`render()`</mark>](#user-content-fn-1)[^1] qui permet au Controller de récupérer une Vue et d'en afficher le contenu. \
On passe alors à la méthode des paramètres qui constituent le contenu de la Response.

{% code overflow="wrap" %}
```php
public function index(): Response
{
    $maResponse = 'Ma Response';
//récupération du Template et affectation de la variable $maResponse qui pourra être invoquée dans le template de cette façon {{ variable }}.
    return $this->render('default/index.html.twig', 
        ['variable' => $maResponse]
    );
}
```
{% endcode %}

### En théorie

La Reponse peut contenir jusqu'à trois arguments : le contenu de la Reponse, le status code et un tableau d'en-têtes HTTP.

Pour définir les trois arguments, la syntaxe est la suivante :

```php
//création de l'objet Response
$response = new Response(
    'Content',
    Response::HTTP_OK,
    ['content-type' => 'text/html']
);
```

Les arguments peuvent être manipulés après la création de la Reponse :&#x20;

```php
$response->setContent('Hello World');

// the headers public attribute is a ResponseHeaderBag
$response->headers->set('Content-Type', 'text/plain');

$response->setStatusCode(Response::HTTP_NOT_FOUND);
```



[^1]: La méthode render est définie dans la Class AbstractController qui est native à Symfony et dont le Controller doit hériter.
