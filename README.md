# SYMGUIDE

Guide de démarrage avec Symfony

Pour commencer il faut mettre en place notre environnement de travail pour utiliser avec symfony :

PHP 8.1+
Git (Configuré avec notre email et notre nom)
Composer
MySQL ou PostgreSQL
Symfony CLI (Installation avec **scoop** ou **homebrew** ou **apt**)

Dans votre éditeur de code (VSCode) installez les extensions suivantes :

- Symfony Pack (Steven Dubois)
- Twig Language 2 (mblode)
- Twig Code Snippets (Nadim Al Abdou)
- PHP Namespace Resolver (Mehedi Hassan)

Les plus :
- GitMoji (Seaton Jiang)
- Git Graph (mhutchie) ou GitLens
- GitCopilot (GitHub)

Note importante concernant le terminal :
Toujours utiliser les commandes dans le dossier de votre projet en dehors da la création d'un nouveau projet.

## Création d'un projet Symfony

Créer un projet d'application web avec la commande suivante :

```bash
symfony new nom-du-projet --webapp
```

Créer un projet d'API avec la commande suivante :

```bash
symfony new nom-du-projet
```

Suite à cela tapez la commande `cd nom-du-projet` pour vous rendre dans le dossier du projet puis lancez la commande `code .` pour ouvrir le projet dans VSCode.

Vous voici prêt à commencer votre projet Symfony, tout lancez la commande `symfony serve -d` pour lancer le serveur de développement. Rendez-vous sur l'adresse `127.0.0.1:8000` pour voir votre projet.

---

## Préparation du projet

Assurez-vous d'avoir au moins réalisé en amont :

- Les diagrammes UML (séquence, classes au minimum)
- Les assets (images, vidéos, sons, etc.)
- Les vues HTML (maquettes UI)
- Créer un projet sur ![Platform.sh](https://platform.sh) (pour le déploiement)*

Avec tout cela vous augmentez les chance d'aboutir à une application livrable et fonctionnelle.


* Platform.sh est un service de déploiement continu pour les applications web. Il permet de déployer automatiquement votre application à chaque push sur la branche principale de votre dépôt Git. Il est gratuit pour les projets Open Source et les étudiants.

---

## Création d'une entité

Pour créer une entité il faut d'abord s'assurer de plusieurs choses :

- Avoir créé une base de données, pour ce faire il faut se rendre dans le fichier `.env` et modifier la ligne `DATABASE_URL` avec les informations de votre base de données. Dans le cas d'un projet situé sur Platform.sh il faudra utiliser un fichier `.env.local` pour ne pas écraser les informations de connexion à la base de données de production. IMPORTANT, privilégiez l'utilisation de PostgreSQL à MySQL.
- N'oublie de faire un `composer install` pour installer les dépendances du projet dans le cas où vous avez cloné un projet existant.

Pour créer une entité il faut utiliser la commande suivante :

```bash
symfony console make:entity

# ou

symfony console make:entity NomDeLentite
```

Cette commande va vous poser plusieurs questions, répondez-y en fonction de vos besoins*. Une fois l'entité créée il faut la migrer dans la base de données avec la commande suivante :

```bash
symfony console make:migration
```

puis executez la migration avec la commande suivante :

```bash
symfony console doctrine:migrations:migrate

ou 

symfony console d:m:m
```

Une fois que nos entités sont créées et migrées dans la base de données il faut les utiliser dans notre code. Pour ce faire nous aurons besoin de créer des contrôleurs en fonction de nos besoins.


*Les questions posées par la commande `make:entity` sont les suivantes :

- Le nom de l'entité
- Le type de la propriété :
  
| type | desc | conseils |
| --- | --- | --- |
| string | Chaine de caractères | |
| text | Chaine de caractères longue | |
| integer | Nombre entier | |
| float | Nombre à virgule | |
| boolean | Booléen | |
| datetime | Date et heure | |
| datetime_immutable | Date et heure (immutable) | |
| date | Date | |
| time | Heure | |
| array | Tableau | |
| json | JSON | |

Il y en a d'autres, vous pouvez les consulter en tapant `?` dans votre terminal en réponse à la question du type de la propriété.

### Les relations

Les relation sont des liens entre les entités. Il existe plusieurs types de relations.
Définnisez les relations en prenons en compte le point du vue de l'entité que vous en train de manipuler. Voici les relations possibles:

| Relation | Description | Exemple |
| --- | --- | --- |
| OneToOne | Une entité est liée à une instace d'une autre entité | Un utilisateur est lié à un profil donc un profil est lié à un utilisateur |
| OneToMany ou ManyToOne | Une entité est liée à plusieurs instances d'une autre entité | Un auteur est lié à plusieurs articles ET plusieurs articles sont liés à un auteur |
| ManyToMany | Une entité est liée à plusieurs instances d'une autre entité ET une entité est liée à plusieurs instances d'une autre entité | Un utilisateur peut avoir plusieurs rôles ET un rôle peut être attribué à plusieurs utilisateurs |
