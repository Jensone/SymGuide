---
description: L'installation de Symfony
---

# Débuter avec Symfony

Vous avez décidé de vous lancer dans le développement d'une application web avec Symfony ? Génial ! Mais avant de commencer, il va falloir s'assurer que vous avez quelques pré-requis :

- Savoir coder en PHP Orienté Objet
- Avoir des les bases en SQL
- C'est tout, pour le moment.

# Comment installer Symfony sur son ordinateur ?

Tout d'abord, il faut savoir que Symfony est un framework PHP. Il va donc falloir installer `PHP 8.1` minimum sur votre ordinateur si vous ne l'avez pas déjà.
Côté Base de données SQL, Symfony est compatible avec les suivantes :

- MySQL
- PostgreSQL
- SQLite
- MariaDB

Pas de recommandation particulière, choisissez celle qui répond le mieux aux besoins de votre projet.

---

## Composer pour commencer

Composer est un gestionnaire de dépendances pour PHP. Il va vous permettre d'installer des librairies PHP dans votre projet Symfony. Symfony CLI va s'appuyer sur Composer pour installer les dépendances de votre projet.

Pour installer Composer, rendez-vous sur le site officiel : [https://getcomposer.org/download/](https://getcomposer.org/download/)

Testez votre installation en tapant dans votre terminal :

```bash
composer
```
Si le terminal vous affiche une liste de commandes, c'est que tout est bon ! Dans le cas contraire vous aurez peut-être besoin de redémarrer votre terminal, voir votre ordinateur.

---

## Symfony CLI

En réalité vous n'allez pas installer Symfony, mais **Symfony CLI**. C'est un outil qui va vous permettre de créer des projets Symfony, de les lancer, de les mettre à jour, etc. C'est un peu comme un couteau suisse pour Symfony dans un environnement de développement. Cela vous apportera une meilleure expérience de développement (DX).

CLI signifie **Command Line Interface**, c'est à dire une interface en ligne de commande. C'est un outil qui va vous permettre d'interagir avec Symfony via votre terminal (bash, zsh, powershell, etc).

Installer Symfony CLI est très simple :

Sur Windows, vous avez besoin de Scoop. Suivez les instruction sur le site officiel : [https://scoop.sh/](https://scoop.sh/). Une fois installé, ouvrez votre terminal et tapez :

```bash
scoop install symfony-cli
```

Sur Mac, vous avez besoin de Homebrew, ouvrez votre terminal et tapez :

```bash
brew install symfony-cli
```

Sur Linux, ouvrez votre terminal et tapez :

```bash
wget https://get.symfony.com/cli/installer -O - | bash
```

Testez votre installation en tapant dans votre terminal :

```bash
symfony
```

C'est idem que pour composer : si le terminal vous affiche une liste de commandes, c'est que tout est bon ! Dans le cas contraire...
