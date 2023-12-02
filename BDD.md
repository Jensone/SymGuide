---
description: Les bases de données avec Symfony
---

# Les bases de données

# Pourquoi faire des bases de données ?

La question devrait plutôt être : mon application a-t-elle besoin de stocker des données ? Si oui, alors il faut utiliser une base de données. Si non, alors il n'y a pas besoin de base de données. Une fois que l'on a décidé d'utiliser une base de données, il faut choisir laquelle. Il existe plusieurs types de bases de données avec lesquel on peut travailler dans Symfony.

## Les bases de données relationnelles

Les bases de données relationnelles sont les plus utilisées. Elles permettent de stocker des données dans des tables. Ces tables sont liées entre elles par des relations. Les bases de données relationnelles les plus utilisées sont MySQL, PostgreSQL, SQLite et Microsoft SQL Server.

## Les bases de données NoSQL

NoSQL signifie "Not only SQL". Ces bases de données sont différentes des bases de données relationnelles. Elles ne stockent pas les données dans des tables. Elles sont plus flexibles que les bases de données relationnelles. Les bases de données NoSQL les plus utilisées sont MongoDB, Redis et Cassandra.

## PostgreSQL

Dans ce guide, nous allons utiliser PostgreSQL. Pourquoi ? Parce que c'est une base de données relationnelle et que c'est la base de données la plus utilisée avec Symfony. Autres raisons :
- Elle est aussi très utilisée dans le monde professionnel. 
- Elle est gratuite et open source. 
- Elle est très performante et très fiable. 
- Elle est compatible avec la plupart des systèmes d'exploitation. 
- Elle est très sécurisée et extensible. 
- Elle est très facile à utiliser et administrer. 
- Elle est très facile à configurer et maintenir. 
- Elle est très facile à mettre à jour. 
- Elle est très facile à déployer, migrer et sauvegarder. 

Ça fait beaucoup de raisons, non ? Je rappelle que c'est pour l'exemple, aucune intention de vous faire adopter PostgreSQL. Utilisez la base de données qui répond le mieux aux besoins de votre application.

### Configuration de PostgreSQL avec Symfony

Pour utiliser PostgreSQL avec Symfony, il faut configurer la base de données dans le fichier `.env` ou `.env.local` :

```bash
# .env
DATABASE_URL=postgresql://db_user:db_password@db_host:db_port/db_name
```

Une fois le fichier mis à jour, il faut créer la base de données. Rendez-vous dans le terminal et tapez la commande suivante :

```bash
symfony console doctrine:database:create
```

Tu peux aussi utiliser le raccourci `d:d:c` qui équivaut à `doctrine:database:create`. Ça y est, la base de données est créée. Tu peux vérifier dans ton interface de base de données (pgAdmin, tableplus, etc.).

