---
description: Déployer une application Symfony sur un serveur de production
---

# Le déploiement

# Pourquoi déployer une application Symfony ?

## Préparation du serveur de production

- Ratacher un nom de domaine au serveur
- Indiquer au serveur de production le dossier `public` comme cible de la racine de l'application
- Créer une base de données correspondant idéalement au projet

---

## Préparation du projet en local

- Réinitialser les migrations avec un seul fichier de version, afin de les migrer en une seule fois sur le serveur de production
- Compiler les éléments nécessaires à la production (assets, webpack, etc.)
- Renseignez les information du serveur de base de données dans le fichier `.env` 
- Ajouter les informations pour le MAILER_DSN dans le fichier `.env`
- Passer l'envirronement en `prod` dans le fichier `.env`
- Mettre en place le fichier `.htaccess` avec la commande `composer require symfony/apache-pack`
- Commit et push de l'ensemble du projet sur GitHub. Veiller à ce que la branche principale soit celle de production. Cela permettre de cloner le projet sur le serveur de production avec la commande `git clone`.

## Dépoloiement du projet sur le serveur de production

- Cloner le projet sur le serveur de production avec la commande `git clone`
- Renommer le dossier du projet avec le nom de domaine (voir avec l'interface Cpanel ou Plesk par exemple).
- Modifier le fichier `.env` avec l'environnement de production
- Rendez-vous dans le terminal du serveur de production et se rendre dans le dossier du projet et réaliser les commandes suivantes :
    - `composer install`
    - `php bin/console d:m:m`
    - `APP_ENV=prod APP_DEBUG=0 php bin/console cache:clear`
    - `php bin/console cache:warmup`
    - `composer install --no-dev --optimize-autoloader`
- Vérifier que l'application est bien en ligne
- Dans le cas ou une erreur se produit voici les précautions :
  - Erreur ^500 : Réactiver le mode `dev` afin de voir l'erreur et la corriger
  - Erreur ^400 : Votre application ne pointe pas sur le bon dossier, vérifier que la racine de l'application est bien le dossier `public`