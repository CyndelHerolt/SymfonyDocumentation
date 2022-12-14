---
description: >-
  Le Controller est une Class qui contient différentes méthodes. Chaque méthode
  correspond à une route particulière et retourne une vue ou des données, entre
  autres.
---

# Introduction

### Quelle fonction pour le Controller ?

Recevoir les données entrées par l'utilisateur et communiquer les changements aux[ modèles](broken-reference) mais également communiquer avec les [modèles](broken-reference) pour obtenir des informations qu'il pourra ensuite transférer aux [vues](broken-reference).\
C'est une fonction PHP qui récupère l'information depuis l'objet Request d'une requête HTTP, puis crée et retourne une réponse HTTP (un objet Response Symfony). La réponse peut être une page HTML, un document XML un tableau JSON, une image, une redirection, une erreur 404, ou n'importe quoi d'autre.

C'est sur cette architecture que repose Symfony ; toutes les Request passent par un premier Controller, le [<mark style="color:yellow;">**Front Controller**</mark>](#user-content-fn-1)[^1] qui va identifier le Controller spécifique à la Request et y rediriger le traitement.

<figure><img src="../.gitbook/assets/MVC_Controller_Model (1).png" alt=""><figcaption><p>Schéma du système qui régit le fonctionnement de Symfony</p></figcaption></figure>

### Conventions d'usage

Dans le cas idéal, le Controller doit contenir le minimum de code possible (20 lignes maximum selon les standards de Symfony). Il ne doit que faire le lien entre les différents éléments de l'application et une réponse.

Le Controller contient des méthodes, chacune, en général, associée à une route.

Il est indispensable de lier le Controller à une route, sans quoi il sera impossible de l'exploiter.

Le dossier /src contient la totalité des Controllers, organisés dans des sous-dossiers.

Aucun traitement de données, accès à la base de données ne doit se faire depuis un Controller.



[^1]: Agit comme un aiguilleur. Dans le squelette de Symfony ce rôle est tenu par le fichier index.php dans le dossier /public. C’est le premier script PHP qui est executé lors du traitement d’une requête.
