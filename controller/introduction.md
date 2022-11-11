# Introduction

### Quelle fonction pour le controller ?

Recevoir les données entrées par l'utilisateur et communiquer les changements aux[ modèles](broken-reference) mais également communiquer avec les [modèles](broken-reference) pour obtenir des informations qu'il pourra ensuite transférer aux [vues](broken-reference).\
C'est une fonction PHP qui récupère l'information depuis l'objet Request d'une requête HTTP, puis crée et retourne une réponse HTTP (un objet Response Symfony). La réponse peut être une page HTML, un document XML un tableau JSON, une image, une redirection, une erreur 404, ou n'importe quoi d'autre.

### Conventions d'usage

Dans le cas idéal, le Controller doit contenir le minimum de code possible (20 lignes maximum selon les standards de Symfony). Il ne doit que faire le lien entre les différents éléments de l'application et une réponse.

Le Controller contient des méthodes, chacune, en générale, associée à une route.

Il est indispensable de lier le Controller à une route, sans quoi il sera impossible de l'appeler.

Le dossier /src contient la totalité des Controllers, organisés dans des sous-dossiers.

Aucun traitement de données, accès à la base de données ne doit se faire depuis un Controller.

