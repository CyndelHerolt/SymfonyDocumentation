---
description: La route permet de lier des URL à des Actions de Controller.
---

# Introduction

### Quelle fonction pour la Route ?

A la réception d'une Request, une Action est appelée afin de générer une Response. La Route va définir quelle Action executer pour l'URL reçue.\
Cela signifie que lorsqu'un utilisateur accède à cette route, l'Action associée dans le Controller sera executée.\
Elle est également nécessaire générer des URL orientées SEO.\
Les Routes peuvent être configurées en YAML, XML, PHP ou par l'utilisation d'Attributs.

### Conventions d'usage

Il est recommandé de définir les Routes sous la forme d'Attributs afin que le Controller et la Route qui lui est propre soient accessibles au même endroit.

Mais il est également possible de définir les Routes de manière centralisée dans un fichier de configuration spécifique.
