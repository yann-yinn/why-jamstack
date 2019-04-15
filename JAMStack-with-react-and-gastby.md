# Architecture JAMStack avec React et Gatsby

**React n'est pas SEO-friendly**. Aujourd'hui, les contenus des sites codés en React ne sont pas visibles par les moteurs de recherches dès lors qu'il y a plusieurs pages gérées par un *routeur* (un test de visite avec *google search console* affiche une page vide). 

Une manière de transformer ce problème en avantage majeur pour un projet est d'utiliser [**Gatsby**](https://www.gatsbyjs.org/): il permet de créer un site *JAMStack* avec React. 

Gatsby.js connaît un succès croissant (34000 ⭐ sur [github](https://github.com/gatsbyjs/gatsby)), il est utilisé pour générer la documention de React, et c'est maintenant une entreprise qui a levé 4 millions de dollars en mai 2018; preuve de l'intérêt du secteur informatique pour les avantages offerts par ce type d'architecture web.

## Avantages d'une Architecture JAMStack : SEO, rapidité, sécurité, scalabilité

JAMStack est une *architecture web* conçue pour offrir au visiteur une expérience ultra-rapide, d'excellents résultats en SEO et pour allèger la charge de travail technique liée à scalabilité et sécurisation d'un serveur web et de sa base de données.

On peut citer parmi les autres avantantages: 

- Préchargement des autres pages pendant la visite d'une page
- Optimisation automatique des images (recoupe, lazy-loading et image "floue" en attendant le chargement complet)
- Un déploiement très facile et rapide sur n'importe quel serveur: il suffit d'uploader des fichiers statiques html; CSS, et JS.
- Pouvoir revenir en un clic à un déploiement précédent du site
- Possible de faire du "A/B" testing en faisant atterir les visiteurs tantôt sur l'une ou l'autre version du site
- Possible d'avoir une prévisualisation complète du site avant publication définitive des nouveaux contenus.

![](https://raw.githubusercontent.com/yann-yinn/why-jamstack/master/images/ligthouse.png?token=AAUeh8-GslHUXclNnzgWHf32Z1d15ELqks5cvZ2lwA%3D%3D)
> Ci-dessus le résultat d'un audit [lighthouse](https://developers.google.com/web/tools/lighthouse) sur le site https://popcorn-nantes.github.io basé sur une architecture JAMStack

## Comment ça marche ?

Contrairement à un site web classique où chaque page est *recalculée à chaque visite* en interrogeant un serveur, qui lui-même interroge une base de données (obligeant en général à la mise en place d'une infrastructure dédiée à la gestion du cache), **Gatsby génère toutes les pages à l'avance** en interrogeant les différents webservices fournisseurs de contenus et de données pour le site. Ces pages pré-générées sous formes de fichiers statiques HTML, JS et CSS sont spécialement optimisées pour offrir une performance maximale aux visiteurs. Il suffit ensuite placer ces fichiers statiques directement sur un "Content Delivery Network" (CDN) pour obtenir un site dont les pages sont servies de manières performantes et facilement scalable à l'échelle mondiale.

## Considérations techniques sur Gatsby, un "Néo-GSS" 

Gatsby fait partie d'une nouvelle génération de **générateur de site statique** (GSS), basé sur l'interrogation d'APIs et les webservices pour obtenir contenus et données; et dont le html est généré à partir de librairies front-end modernes telles que React. 

Le résultat produit par Gatsby est une "SPA" (single page application) composés de simples fichier statiques HTML, CSS et JS. Bien que chacune des pages soient pré-générées en html, dès lors qu'on visite une page c'est bien React qui reprend entièrement la main en "hydratant" le html avec son JavaScript, offrant ainsi une expérience sans rechargement de page à l'utilisateur. C'est donc au final l'expérience d'une application React classique mais avec en prime des données "pré-chargées" lors de la phase de compilation pour accélérer la navigation.

### Déploiement et re-génération des pages quand les contenus sont mis à jour

La commmande `gatsby build` permet de compiler le site dans un dossier `dist`, à partir de ses fichiers source (dossier `src`). Il suffit de déployer ce dossier compilé `dist` pour mettre le site en ligne. 

Un serveur d'intégration continue peut par exemple être utilisé pour créer automatiquement ce build à chaque commit sur la branche `master` et automatiser le déploiement de manière personnalisée.

A chaque changement de contenu, il faut "reconstruire" le site en entier pour "publier" les changements. Pour rendre cela transparent pour les rédacteurs et rédactrices de contenus, il est suffit de "pinguer" une url qui déclenchera la re-génération du site sur le serveur de build au moment de la création / mise à jour / suppression d'un article  (on parle de  *webhook*)

Cela peut prend quelques minutes pour reconstruire la version buildée du site. Cette phase de compilation du site a une contre-partie intéressante : les déploiement deviennent *atomiques* : on veut dire par là que ce système permet de revenir à la version précédente du site, contenus compris, simplement en revenant à la version précédente des fichiers de build. 

### Hébergeurs spécialisés JAMStack

A noter qu'il existe de plus en plus d'hébergeurs pour automatiser toutes les étapes ci-dessus et les déploiements d'un site JAMStack. A partir d'un simple dépôt Git, [*Netlify*](https://www.netlify.com/) permet par exemple de re-générer son site à chaque push, de ré-déclencher un build par simple ping d'une URL déjà founie, d'avoir une interface de rollback, des logs détaillés, d'avoir des branches de prévisualisation, l'A/B testing etc. Netlify permet même d'uploader un dossier contenant des fonctions lambdas nodejs et les déploie automatiquement sur AWS.

### Les limites de JAMStack

Tout est question de compromis en informatique: 

- Gatsby n'est pas optimisé pour un site qui devrait générer un million de pages toutes les 5 minutes...
- Un site de type intranet ou back-office, qui contient uniquement des pages dont l'affichage dépend des droits et du rôle de la personne connecté, ne pourra pas être réalisé de cette manière car il n'y aura pas de page "type" à pré-générer.
- Un site basé uniquement sur des résultats de recherche ou des filtres de recherche (ex : Airbnb) n'aura probablement pas d'intérêt à utiliser une telle technologie.




