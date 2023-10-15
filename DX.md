---
description: Créer une véritable DX ou Developer eXperience
---

# DX ou Developer eXperience

On vous répète souvent "l'expérience utilisateur c'est important", mais qu'en est-il de l'expérience développeur ? C'est ce que l'on appelle la DX ou Developer eXperience.

# Pourquoi la DX est importante ?

La DX est importante pour plusieurs raisons :

- La DX permet de gagner du temps
- La DX permet de gagner en qualité
- La DX permet de gagner en confort
- La DX permet de gagner en sérénité
- La DX permet de gagner en sécurité

En résumé ce gain de temps, de qualité, de confort, de sérénité et de sécurité se réalise grâce à l'automatisation de tâches répétitives et fastidieuses, l'automatisant des tests, en facilitant la mise en place de l'environnement de développement, en facilitant la mise en place de l'environnement de production, etc. Alors ne négligez pas la DX, elle est importante !

## Symfony CLI

Cet outil est un excellent exemple de DX. Ré-écrire le même code est contraignant et fastidieux. Symfony CLI. Il permet de créer un projet Symfony en une seule commande. Il permet aussi de lancer un serveur web local ou encore un serveur de logs en une seule commande.

Voici la liste des commandes en fonction de vos projets d'applications. Pour les executer, il suffit de taper `symfony` ou `php bin/console` suivi de la commande :

| Commandes | Description |
| :--- | :--- |
| check:requriments | Vérifier les prérequis de votre ordinateur |
| new | Créer un nouveau projet Symfony |
| server | Lancer le serveur web local avec les logs |
| server:start -d | Lancer le serveur web local sans bloquer le terminal |
| server:stop | Arrêter le serveur web local |
| about | Affiche des informations sur le projet en cours |
| completion | Génère le script de complétion pour le shell |
| help | Affiche l'aide pour une commande |
| list | Liste les commandes disponibles |
| assets:install | Installe les ressources web du bundle dans un répertoire public |
| cache:clear | Vide le cache |
| cache:pool:clear | Vide les pools de cache |
| cache:pool:delete | Supprime un élément d'un pool de cache |
| cache:pool:invalidate-tags | Invalide les tags de cache pour tous les pools ou un pool spécifique |
| cache:pool:list | Liste les pools de cache disponibles |
| cache:pool:prune | Purge les pools de cache |
| cache:warmup | Préchauffe un cache vide |
| config:dump-reference | Affiche la configuration par défaut d'une extension |
| dbal:run-sql | Exécute une requête SQL arbitraire depuis la ligne de commande |
| debug:autowiring | Liste les classes/interfaces utilisables pour l'autowiring |
| debug:config | Affiche la configuration actuelle d'une extension |
| debug:container | Affiche les services actuels d'une application |
| debug:dotenv | Liste tous les fichiers dotenv avec leurs variables et valeurs |
| debug:event-dispatcher | Affiche les écouteurs configurés pour une application |
| debug:firewall | Affiche des informations sur les pare-feu de sécurité |
| debug:form | Affiche des informations sur les types de formulaires |
| debug:messenger | Liste les messages pouvant être envoyés via les bus de messages |
| debug:router | Affiche les routes actuelles d'une application |
| debug:serializer | Affiche des informations sur la sérialisation des classes |
| debug:translation | Affiche des informations sur les messages de traduction |
| debug:twig | Affiche une liste des fonctions, filtres, globales et tests Twig |
| debug:validator | Affiche les contraintes de validation pour les classes |
| doctrine:cache:clear-collection-region | Vide la région de cache de collection du second niveau |
| doctrine:cache:clear-entity-region | Vide la région de cache d'entité du second niveau |
| doctrine:cache:clear-metadata | Vide le cache de métadonnées des différents pilotes de cache |
| doctrine:cache:clear-query | Vide le cache de requêtes des différents pilotes de cache |
| doctrine:cache:clear-query-region | Vide la région de cache de requête du second niveau |
| doctrine:cache:clear-result | Vide le cache de résultats des différents pilotes de cache |
| doctrine:database:create | Crée la base de données configurée |
| doctrine:database:drop | Supprime la base de données configurée |
| doctrine:ensure-production-settings | Vérifie que Doctrine est correctement configuré pour un environnement de production |
| doctrine:mapping:convert | Convertit les informations de mapping entre différents formats pris en charge |
| doctrine:mapping:import | Importe les informations de mapping depuis une base de données existante |
| doctrine:mapping:info | Affiche des informations de base sur toutes les entités mappées |
| doctrine:migrations:current | Affiche la version actuelle des migrations |
| doctrine:migrations:diff | Génère une migration en comparant la base de données actuelle avec les informations de mapping |
| doctrine:migrations:dump-schema | Dump la structure de la base de données vers une migration |
| doctrine:migrations:execute | Exécute une ou plusieurs versions de migration manuellement |
| doctrine:migrations:generate | Génère une classe de migration vide |
| doctrine:migrations:latest | Affiche la dernière version des migrations |
| doctrine:migrations:list | Affiche la liste de toutes les migrations disponibles et leur statut |
| doctrine:migrations:migrate | Exécute une migration vers une version spécifiée ou la dernière version disponible |
| doctrine:migrations:rollup | Rassemble les migrations en supprimant toutes les versions suivies et en n'insérant que la version existante |
| doctrine:migrations:status | Affiche l'état d'un ensemble de migrations |
| doctrine:migrations:sync-metadata-storage | S'assure que le stockage des métadonnées est à la dernière version |
| doctrine:migrations:up-to-date | Indique si le schéma est à jour |
| doctrine:migrations:version | Ajoute et supprime manuellement des versions de migration depuis la table des versions |
| doctrine:query:dql | Exécute une requête DQL arbitraire depuis la ligne de commande |
| doctrine:query:sql | Exécute une requête SQL arbitraire depuis la ligne de commande |
| doctrine:schema:create | Traite le schéma et le crée directement sur le stockage de l'EntityManager ou génère la sortie SQL correspondante |
| doctrine:schema:drop | Supprime le schéma de base de données complet de l'EntityManager ou génère la sortie SQL correspondante |
| doctrine:schema:update | Exécute (ou génère) le SQL nécessaire pour mettre à jour le schéma de la base de données en fonction des métadonnées de mapping actuelles |
| doctrine:schema:validate | Valide les fichiers de mapping |
| lint:container | Vérifie que les arguments injectés dans les services correspondent aux déclarations de type |
| lint:twig | Vérifie la syntaxe d'un template Twig et affiche les erreurs rencontrées |
| lint:xliff | Vérifie la syntaxe d'un fichier XLIFF et affiche les erreurs rencontrées |
| lint:yaml | Vérifie la syntaxe d'un fichier YAML et affiche les erreurs rencontrées |
| mailer:test | Teste les transports Mailer en envoyant un email |
| make:auth | Crée un authenticateur Guard de différents types |
| make:command | Crée une nouvelle classe de commande console |
| make:controller | Crée une nouvelle classe de contrôleur |
| make:crud | Crée les opérations CRUD pour une classe d'entité Doctrine |
| make:docker:database | Ajoute un conteneur de base de données à votre fichier docker-compose.yaml |
| make:entity | Crée ou met à jour une classe d'entité Doctrine, et éventuellement une ressource API Platform |
| make:fixtures | Crée une nouvelle classe pour charger des fixtures Doctrine |
| make:form | Crée une nouvelle classe de formulaire |
| make:message | Crée un nouveau message et son gestionnaire |
| make:messenger-middleware | Crée un nouveau middleware Messenger |
| make:migration | Crée une nouvelle migration basée sur les changements de la base de données |
| make:registration-form | Crée un nouveau système de formulaire d'inscription |
| make:reset-password | Crée un contrôleur, une entité et des référentiels pour une utilisation avec symfonycasts/reset-password-bundle |
| make:security:form-login | Génère le code nécessaire pour l'authentification form_login |
| make:serializer:encoder | Crée une nouvelle classe d'encodeur pour le sérialiseur |
| make:serializer:normalizer | Crée une nouvelle classe de normalisateur pour le sérialiseur |
| make:stimulus-controller | Crée un nouveau contrôleur Stimulus |
| make:subscriber | Crée une nouvelle classe d'abonné d'événements |
| make:test | Crée une nouvelle classe de test |
| make:twig-component | Crée un composant Twig (ou Live) |
| make:twig-extension | Crée une nouvelle extension Twig avec sa classe runtime |
| make:user | Crée une nouvelle classe d'utilisateur de sécurité |
| make:validator | Crée une nouvelle classe de validateur et de contrainte |
| make:voter | Crée une nouvelle classe de votant de sécurité |
| messenger:consume | Consomme des messages |
| messenger:failed:remove | Supprime les messages donnés du transport d'échec |
| messenger:failed:retry | Réessaie un ou plusieurs messages depuis le transport d'échec |
| messenger:failed:show | Affiche un ou plusieurs messages du transport d'échec |
| messenger:setup-transports | Prépare l'infrastructure requise pour le transport |
| messenger:stats | Affiche le nombre de messages pour un ou plusieurs transports |
| messenger:stop-workers | Arrête les travailleurs après leur message actuel |
| router:match | Aide au débogage des routes en simulant une correspondance de chemin d'informations |
| secrets:decrypt-to-local | Déchiffre tous les secrets et les stocke dans le coffre local |
| secrets:encrypt-from-local | Chiffre tous les secrets locaux dans le coffre |
| secrets:generate-keys | Génère de nouvelles clés de chiffrement |
| secrets:list | Liste tous les secrets |
| secrets:remove | Supprime un secret du coffre |
| secrets:set | Définit un secret dans le coffre |
| security:hash-password | Hash un mot de passe utilisateur |
| server:dump | Démarre un serveur de dump qui collecte et affiche les dumps en un seul endroit |
| server:log | Démarre un serveur de journalisation qui affiche les journaux en temps réel |
| translation:extract | Extrait les clés de traduction manquantes du code vers les fichiers de traduction |
| translation:pull | Récupère les traductions à partir d'un fournisseur donné. |
| translation:push | Envoie les traductions vers un fournisseur donné. |


