# Structure

Un Contoller doit être construit en suivant une structure définie.&#x20;

1. Préciser que c'est un Controller : \
   &#x20;<mark style="color:red;">**`namespace`**</mark>`App\Controller`
2. Importer les Class à exploiter : \
   &#x20;<mark style="color:red;">**`use`**</mark>`Chemin\Menant\A\La\Class`
3. Le contenu executé lors de l'appel du Controller doit se trouver dans une Class qui doit porter le même nom que le Controller : \
   &#x20;<mark style="color:red;">`class`</mark><mark style="color:orange;">`NomController`</mark>` ``{ ... }`
4. Dans cette Class, initialiser la Route grace à cet attribut : \
   &#x20;`#[`<mark style="color:purple;">`Route`</mark>`(`<mark style="color:blue;">`'/'`</mark>`, name:`<mark style="color:blue;">`'app_name'`</mark>`)]`
5. Et on rédige la fonction qui sera executée à l'appel du Controller en spécifiant l'objet Response : \
   <mark style="color:red;">`public function`</mark><mark style="color:purple;">`nomFonction`</mark>`(`<mark style="color:blue;">`$parametres`</mark>`):`<mark style="color:orange;">`Response`</mark>`{ ... }`
6. Récupérer la valeur de retour de la fonction pour la traiter ailleurs : \
   <mark style="color:red;">`return`</mark>`( ... )`

**Exemple :** Ici un Controller permettant de générer un nombre aléatoire.

{% code title="/src/Controller/LuckyController.php" overflow="wrap" lineNumbers="true" %}
```php
<?php

//Précise la nature du code, ici un Controller
namespace App\Controller;

//Importe les différentes Class externes qui seront utilisées dans le Controller
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Annotation\Route;

//Ensemble de code contenant des variables et des fonctions permettant de créer des objets
class LuckyController
{
//attribut qui permet de diriger une url (ou un pattern d'url) vers une méthode de controller
    #[Route('/lucky/number/{max}', name: 'app_lucky_number')]
//fonction executée à l'appel du controller
    public function number(int $max): Response
    {
        $number = random_int(0, $max);
//retourne une valeur qui sera exploitable après l'execution de la fonction
        return new Response(
            '<html><body>Lucky number: '.$number.'</body></html>'
        );
    }
}
```
{% endcode %}

