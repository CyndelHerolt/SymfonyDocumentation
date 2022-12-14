---
description: La route permet de diriger une URL (ou un pattern d'URL) vers une Action.
---

# Introduction

### Quelle fonction pour la Route ?

A la réception d'une Request, une Action est appelée afin de générer une Response. La Route va définir quelle action effectuer pour l'URL reçue. Elle est également nécessaire générer des URL orientées SEO.\
Les Routes peuvent être configurées en YAML, XML, PHP ou par l'utilisation d'Attributs.

### Conventions d'usage

Il est recommandé de définir les Routes sous la forme d'Attributs afin que le Controller et la Route qui lui est propre soit accessibles au même endroit.
