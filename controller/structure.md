# Structure

Le Controller est une Class qui contiendra différentes méthodes. Chaque méthode correspondra à une route particulière et retournera une vue ou des données, entre autres.

{% code title="/src/Controller/LuckyController.php" overflow="wrap" lineNumbers="true" %}
```php
<?php

//Précise la nature du code, ici un Controller
namespace App\Controller;

//Importe les différentes Class externes qui seront utilisées dans le Controller
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Annotation\Route;

class LuckyController
{
    #[Route('/lucky/number/{max}', name: 'app_lucky_number')]
    public function number(int $max): Response
    {
        $number = random_int(0, $max);

        return new Response(
            '<html><body>Lucky number: '.$number.'</body></html>'
        );
    }
}
```
{% endcode %}

