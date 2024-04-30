---
description: Des Class PHP pour gérer vos tables
---

# Les Entités

Les entités sont des classes PHP ordinaires qui sont annotées pour indiquer à Doctrine comment les mapper aux tables de la base de données. Vous pouvez définir vos entités dans le répertoire `src/Entity` de votre projet Symfony. Par exemple :

```php
// src/Entity/Product.php

namespace App\Entity;

use App\Repository\AnneeRepository;
use Doctrine\ORM\Mapping as ORM;

#[ORM\Entity(repositoryClass: ProductRepository::class)]
class Product
{

    #[ORM\Id]
    #[ORM\GeneratedValue]
    #[ORM\Column]
    private $id;

   #[ORM\Column(length: 255)]
    private $libelle;

    // Getters et Setters
    public function getId(): ?int
    {
        return $this->id;
    }

    public function setId(?int $id): void
    {
        $this->id = $id;
    }
    
        public function getLibelle(): ?string
    {
        return $this->libelle;
    }

    public function setLibelle(string $libelle): static
    {
        $this->libelle = $libelle;

        return $this;
    }
}

```
