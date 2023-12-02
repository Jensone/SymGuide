---
description: Les fixtures dans Symfony
---

# Les fixtures

# Pourquoi faire des fixtures ?

Pour tester notre application, nous avons besoin de données. Nous pourrions créer des données à la main, mais cela prendrait beaucoup de temps. Nous allons donc utiliser des fixtures.
Les fixtures sont des données fictives que nous allons créer et qui vont nous permettre de tester notre application.

# Installation

Pour installer les fixtures, nous allons utiliser la commande suivante :

```bash
composer require --dev orm-fixtures
```

# Création des fixtures

Pour créer des fixtures, une des méthode populaire est de faire un boucle de instanciation d'objet des entités de l'application puis les persister en base de données.

Pour cela, nous allons coder dans le fichier `src/DataFixtures/AppFixtures.php`. Partons du principe que nous avons une entité `Category` et une entité `Product` avec une relation `OneToMany` entre les deux.

```php
# src/DataFixtures/AppFixtures.php
<?php

// ...
use App\Entity\Category;
use App\Entity\Product;

class AppFixtures extends Fixture
{
    public function load(ObjectManager $manager)
    {
        // Création de 10 catégories
        for ($i = 0; $i < 10; $i++) {
            $category = new Category();
            $category->setName('Category '.$i);
            $manager->persist($category);

            // Création de 10 produits par catégorie
            for ($j = 0; $j < 10; $j++) {
                $product = new Product();
                $product->setName('Product '.$j);
                $product->setPrice(mt_rand(10, 100));
                $product->setCategory($category);
                $manager->persist($product);
            }
        }

        $manager->flush();
    }
}
```

Cet exemple est très simple, mais il est possible de faire des fixtures beaucoup plus complexes. Ici nous voulons créé 10 catégories et 100 produits.

Afin d'exécuter les fixtures, nous allons utiliser la commande suivante :

```bash
php bin/console doctrine:fixtures:load
```

Le raccourci de cette commande est `d:f:l` à la place de `doctrine:fixtures:load`. Il sera possible de reformater la base de données ou d'ajouter des données supplémentaires avec les options `--append`.