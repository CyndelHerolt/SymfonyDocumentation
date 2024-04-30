---
description: >-
  Une gestion avancée des bases de données grâce à son ORM (Object-Relational
  Mapping) appelé Doctrine.
---

# Introduction

La gestion des bases de données dans Symfony repose sur des concepts clés tels que les entités, les repositories, les migrations.

## Configuration de la base de données

Vous devez d'abord configurer les paramètres de connexion à la base de données en utilisant le fichier `.env.local`.&#x20;

{% code overflow="wrap" %}
```bash
# Exemple de configuration pour une base de données MySQL
DATABASE_URL=mysql://user:password@localhost:3306/database_name?serverVersion=version_MySql&charset=utf8
# Exemple de configuration pour une base de données PostgreSQL version 13
DATABASE_URL=postgresql://user:password@localhost:5432/database_name?serverVersion=13
```
{% endcode %}

Cette variable d'environnement sert de point d'entrée vers votre base de données. Mais il faut maintenant la créer.

```bash
# Commande pour créer votre base de données
php bin/console doctrine:database:create
# ou
php bin/console d:d:c
```

Maintenant que votre database est prête, vous pouvez maintenant créer vos tables appelées ici <mark style="color:yellow;">**Entités**</mark>.
