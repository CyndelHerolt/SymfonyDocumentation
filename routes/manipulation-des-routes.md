# Manipulation des Routes

### La création de Route en tant qu'Attribut

La création d'un Attribut de Route de fait juste avant la Methode dans le Controller. Il doit contenir des détails tels que l'URL, le nom de la Route ainsi que les méthodes HTTP autorisées.\
Le nom sera alors utilisé pour générer des liens vers cette Route.

#### Structure de l'Attribut de Route

{% code overflow="wrap" %}
```php
#[Route('/monURL', name:'nom_de_la_Route')]
public function nomFonction(): Response
{
}
```
{% endcode %}

_Une Route contient au minimum un path (URL) et un nom._

On peut y incorporer des paramètres tels que les méthodes HTTP ou des conditions.

{% code overflow="wrap" %}
```php
#[Route('/monURL', name:'nom_de_la_Route', , method: ['GET'],)]
public function nomFonction(): Response
{
}
```
{% endcode %}

Afin d'utiliser les Routes, il faut ajouter cette ligne :&#x20;

{% code overflow="wrap" %}
```php
use Symfony\Component\Routing\Annotation\Route;
```
{% endcode %}

### La création de Route dans un fichier de configuration spécifique

Au lieu de déclarer vos Routes directement dans les Class, il est possible de les définir dans un fichier YAML, XML ou PHP.&#x20;

#### Dans un fichier YAML

{% code overflow="wrap" %}
```yaml
# config/routes.yaml
nom_de_la_Route:
    path: /monURLaml
    # the controller value has the format 'controller_class::method_name'
    controller: App\Controller\controller_class::method_name
    methods:    GET
```
{% endcode %}

#### Dans un fichier PHP

{% code overflow="wrap" %}
```php
// config/routes.php
use App\Controller\ClassController;
use Symfony\Component\Routing\Loader\Configurator\RoutingConfigurator;

return function (RoutingConfigurator $routes) {
    $routes->add('nom_de_la_Route', '/monURL')

        ->controller([ClassController::class, 'method_name']);
        ->methods(['GET'])
};
```
{% endcode %}

{% hint style="info" %}
Par défaut Symfony ne charge que les Routes définies en YAML. Afin de charger le fichier XML ou PHP il est nécessaire de mettre à jour le fichier src/Kernel.php
{% endhint %}

