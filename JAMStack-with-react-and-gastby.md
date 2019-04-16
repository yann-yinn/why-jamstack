# Architecture JAMStack avec React et Gatsby

**React n'est pas SEO-friendly**. Aujourd'hui, les contenus des sites codés en React ne sont pas visibles par les moteurs de recherches dès lors qu'il y a plusieurs pages gérées par un *routeur* (un test de visite avec *google search console* affiche une page vide). 

On peut convertir ce problème en atout en utilisant [**Gatsby**](https://www.gatsbyjs.org/): il permet d'exporter les pages d'une application React sous forme de fichiers statiques html, qui seront indexables sans souci par les moteurs de recherches.  Mais Gatsby va plus loin en offrant aussi les avantages suivants:

- Temps de chargement des pages ultra-rapide qui favorise le SEO
- Optimisation automatique du [chargement des images](https://www.gatsbyjs.org/packages/gatsby-image/).
- Préchargement automatique des autres pages pendant la visite d'une page pour accélérer encore la navigation
- Déploiement du site simplissime : il suffit d'uploader les fichiers statiques
- Sécurité : pas de serveur PHP ou de CMS exposés
- Scalabilité sans effort ni configuration en uploadant les fichiers statiques sur un CDN
- Possibilité de prévisualiser l'ensemble d'un site avant sa publication (branche git de "preview")

![](https://raw.githubusercontent.com/yann-yinn/why-jamstack/master/images/ligthouse.png?token=AAUeh8-GslHUXclNnzgWHf32Z1d15ELqks5cvZ2lwA%3D%3D)
> Ci-dessus le résultat d'un audit [lighthouse](https://developers.google.com/web/tools/lighthouse) sur le site https://popcorn-nantes.github.io basé sur une architecture JAMStack

Gatsby.js connaît un succès croissant (34000 ⭐ sur [github](https://github.com/gatsbyjs/gatsby)), il est utilisé pour générer la documention de React, et c'est aussi désormais une entreprise qui a levé 4 millions de dollars en mai 2018; preuve de l'intérêt du secteur informatique pour les avantages offerts par ce type d'architecture web.

## Comment ça marche ?

Contrairement à un site web classique où chaque page est *recalculée à chaque visite* en interrogeant un serveur, qui lui-même interroge une base de données (obligeant en général à la mise en place d'une infrastructure dédiée à la gestion du cache), **Gatsby génère toutes les pages à l'avance** en interrogeant les différents webservices fournisseurs de contenus et de données pour le site. Ces pages pré-générées sous formes de fichiers statiques HTML, JS et CSS sont spécialement optimisées pour offrir une performance maximale aux visiteurs. Il suffit ensuite placer ces fichiers statiques directement sur un "Content Delivery Network" (CDN) pour obtenir un site dont les pages sont servies de manières performantes et facilement scalable à l'échelle mondiale.

## Gatsby : un générateur de site statique nouvelle génération

Gatsby est **générateur de site statique** basé sur l'interrogation de webservices pour obtenir contenus et données; et dont le html final est généré à partir de React. Pour le visiteur, l'expérience est toutefois bien celle d'une **SPA (single page application)**, sans rechargement de page : bien que chacune des pages soient pré-générées en html, dès lors qu'on visite une page c'est bien React qui reprend entièrement la main en [*hydratant* le html](https://www.gatsbyjs.org/blog/2018-10-15-beyond-static-intro/#hydration). C'est donc au final l'expérience d'une application React classique mais avec en prime des données "pré-chargées" lors de la phase de compilation pour accélérer la navigation.

Puisqu'in fine, il s'agit d'une application React classique, cela signifie qu'il est possible de créer des routes uniquement côté client, sans qu'elles soient pré-rendues en html, comme on le ferait pour une application React classique: https://www.gatsbyjs.org/docs/building-apps-with-gatsby/#client-only-routes--user-authentication


### Déployer et re-générer les pages d'un site Gatsby

La commmande `gatsby build` permet de compiler un site Gatsby dans un dossier `dist`. Il suffit de ensuite de déployer ce dossier compilé `dist` pour mettre le site en ligne. 

On peut confier cette tâche à un serveur de "build". Ce serveur de build sera chargé de déclencher à la compilation lorsqu'un nouveau commit à lieu sur le master, d'exposer un webhook pour permettre de déclencher le build à distance, d'envoyer des mails si une erreur est recontrée pendant le build, de pouvoir redéployer une version précédente du build si besoin etc. 

Pour s'épargner cette configuration, il possible d'utiliser un service spécialisé tel que l'excellent [Netlify](https://www.netlify.com/) qui fait tout cela automatiquement, et offrent en prime d'autres fonctionnalités intéressantes comme les [branches de prévisualisations](https://www.netlify.com/blog/2016/07/20/introducing-deploy-previews-in-netlify/) ou le déploiement automatique de fonctions lambda chez AWS.

Lorsqu'un contenu est modifié dans le CMS ou ailleurs, il suffit de "pinguer" programmatiquement l'url de compilation du serveur de build pour redéployer le site automatiquement. Le nouveau site sera visible en production en quelques minutes.

### Quelques limites à Gatsby

- Gatsby n'est pas optimisé pour un site qui devrait générer un million de pages toutes les 5 minutes, le temps de construction augmente au fur et à mesure du nombres de pages.
- Il ne semble pas y avoir de solution officielle pour le multilingue.




