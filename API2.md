---
description: La création d'une API avec Symfony
---

# Créer une API

Symfony accompagné de API Platform permet de créer des API REST facilement. 

## Pourquoi créer une API ?

Les API sont un élément essentiel de l'architecture d'une application. Elles permettent de communiquer avec d'autres applications, de partager des données, d'utiliser des services aux fonctionnalités variés (paiement, envoi de mail, etc.).

## Comment créer une API avec Symfony ?

Symfony permet de créer des API facilement grâce à l'outil [API Platform](https://api-platform.com/). API Platform est un ensemble d'outils qui permettent de créer des API REST et GraphQL.

Voici les étapes pour créer une API avec Symfony et API Platform :

Créez un projet Symfony depuis votre terminal

```bash
symfony new doctomap
```

Configurez la base de données de votre choix, ici on utilisera SQLite. Commencez par décommenter la ligne `DATABASE_URL="sqlite:///%kernel.project_dir%/var/data.db"` et commenter les autres.

Puis créez la base de données

```bash
symfony console d:d:c
```

Installez le MakerBundle et ORM pour créer des entités

```bash
composer require symfony/maker-bundle --dev
```
Puis on installe le package ORM

```bash
composer require symfony/orm-pack
```

Maintenant, on peut créer notre première entité

```bash
symfony console make:entity Doctor
```

Voici la liste des propriétés de notre entité :

| Nom | Type | Détail | Nullable |
| :--- | :--- | :--- | :--- |
| firstname | string | 50 caractères | Non |
| lastname | string | 50 caractères | Non |
| speciality | string | 50 caractères | Non |
| address | string | 255 caractères | Non |
| city | string | 50 caractères | Non |
| zip | string | 5 caractères | Non |
| phone | string | 12 caractères | Oui |

Voilà maintenant que notre entité est créée, on peut faire la migration

```bash
symfony console make:migration
```

Et on peut lancer la migration

```bash
symfony console d:m:m
```

À ce stade rien de nouveau, on a déjà fait ça plusieurs fois. Passons maintenant à l'installation de API Platform.

```bash
composer require api
```

Ce package va installer plusieurs dépendances dont API Platform Core, API Platform Admin, API Platform Schema Generator, API Platform Migrations et API Platform Doctrine ORM.

On termine la configuration en ajoutant une annotation à notre entité

```php
<?php

// ...

use ApiPlatform\Metadata\ApiResource;

#[ORM\Entity(repositoryClass: DoctorRepository::class)]
#[ApiResource]
class Doctor
{
    // ...
}
```

Rendez-vous sur la page `/api` de votre projet, vous devriez voir une page avec la liste des routes de votre API.

Avant de se quitter, on va ajouter quelques données dans notre base de données. Pour cela, on va créer des données de test avec le package Fixtures et Faker.

```bash
composer require orm-fixtures --dev
```

Puis

```bash
composer require fakerphp/faker
```

Dans le dossier `src/DataFixtures`, insérez le code suivant dans le fichier `AppFixtures.php` et ajoutez-y le code suivant :

```php
<?php

// ...

use App\Entity\Doctor;
use Faker\Factory;

class AppFixtures extends Fixture
{
    public function load(ObjectManager $manager)
    {
        $faker = Factory::create('fr_FR');

        for ($i = 0; $i < 30; $i++) {
            $doctor = new Doctor();
            $doctor->setFirstname($faker->firstName());
            $doctor->setLastname($faker->lastName());
            $doctor->setSpeciality($faker->jobTitle());
            $doctor->setAddress($faker->streetAddress());
            $doctor->setCity($faker->city());
            $doctor->setZip($faker->postcode());
            $doctor->setPhone($faker->phoneNumber());

            $manager->persist($doctor);
        }

        $manager->flush();
    }
}
```

N'oubliez pas d'exécuter la commande suivante pour insérer les données dans la base de données

```bash
symfony console d:f:l
```

On a désormais des données de test dans notre base de données. On peut maintenant les afficher dans notre API !

Et voilà, vous avez créé votre première API avec Symfony et API Platform. Vous pouvez désormais mettre en place des Assertions pour la validation des données, mettre en place des filtres, une pagination ou encore l'authentification avec JWT.

N'oubilez pas de tester votre API avec [Postman](https://www.postman.com/) ou [Insomnia](https://insomnia.rest/).

---

Ressources :

* [Documentation API Platform](https://api-platform.com/)
* [Documentation de Symfony](https://symfony.com/doc/current/the-fast-track/en/26-api.html#installing-api-platform)
* [Documentation de Doctrine](https://www.doctrine-project.org/projects/doctrine-orm/en/2.9/index.html)