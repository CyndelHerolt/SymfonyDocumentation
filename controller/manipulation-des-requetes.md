---
description: >-
  Récuperer et manipuler des éléments provenance de la requête HTTP du client
  (utilisateur ou navigateur)
---

# Manipulation des Requêtes

La manipulation des Requêtes requiert le passage en paramètre d'un Controller, un Objet de type Request => injection de dépendance. \
Il faut alors importer la [Class Request](https://github.com/symfony/symfony/blob/6.1/src/Symfony/Component/HttpFoundation/Request.php) native de Symfony qui permet d'exploiter les requêtes en ajoutant cette ligne :&#x20;

```php
use Symfony\Component\HttpFoundation\Request;
```

Ensuite, la syntaxe est la suivante :&#x20;

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

Les [routes dynamiques](../routes/routes-dynamiques.md) permettent d'exploiter des paramètres



Every HTTP web interaction begins with a request and ends with a response. Your job as a developer is to create PHP code that reads the request information (e.g. the URL) and creates and returns a response (e.g. an HTML page or JSON string). This is a simplified overview of the request workflow in Symfony applications:

1. The **user** asks for a **resource** in a **browser**;
2. The **browser** sends a **request** to the **server**;
3. **Symfony** gives the **application** a **Request** object;
4. The **application** generates a **Response** object using the data of the **Request** object;
5. The **server** sends back the **response** to the **browser**;
6. The **browser** displays the **resource** to the **user**.

Typically, some sort of framework or system is built to handle all the repetitive tasks (e.g. routing, security, etc) so that a developer can build each _page_ of the application. Exactly _how_ these systems are built varies greatly. The HttpKernel component provides an interface that formalizes the process of starting with a request and creating the appropriate response. The component is meant to be the heart of any application or framework, no matter how varied the architecture of that system:
