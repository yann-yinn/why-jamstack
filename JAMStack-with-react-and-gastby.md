# Architecture JAMStack avec React et Gatsby

**React n'est pas SEO-friendly**. Aujourd'hui, les contenus des sites codés en React ne sont pas visibles par les moteurs de recherches dès lors qu'il y a plusieurs pages gérées par un *routeur* (un test de visite avec *google search console* affiche une page vide). 

On peut convertir ce problème en atout en utilisant [**Gatsby**](https://www.gatsbyjs.org/): il permet d'exporter les pages d'une application React sous forme de fichiers statiques html, qui seront indexables sans souci par les moteurs de recherches. Gatsby fait partie des outils modernes permettant de mettre en place une architecture web [JAMStack](https://jamstack.org/) et se concentre sur le fait d'offrir au visiteur **l'expérience de visite la plus rapide possible.**

Parmi les avantages de Gatsby et d'une architecture JAMStack en général:

- Temps de chargement des pages ultra-rapide qui favorise le SEO
- Optimisation automatique du [chargement des images](https://www.gatsbyjs.org/packages/gatsby-image/).
- Préchargement automatique des autres pages pendant la visite d'une page pour accélérer la navigation
- Déploiement du site simplissime : il suffit d'uploader les fichiers statiques
- Moins de faille de sécurité possibles : car il n'y a plus d'application serveur ou de CMS exposé
- Scalabilité mondiale sans effort en uploadant les fichiers statiques directement un CDN
- Possibilité de prévisualiser l'ensemble d'un site avant publication des modifications (branche git de "preview")

![](https://raw.githubusercontent.com/yann-yinn/why-jamstack/master/images/ligthouse.png?token=AAUeh8-GslHUXclNnzgWHf32Z1d15ELqks5cvZ2lwA%3D%3D)
> Ci-dessus le résultat d'un audit [lighthouse](https://developers.google.com/web/tools/lighthouse) sur le site https://popcorn-nantes.github.io basé sur une architecture JAMStack avec [Nuxt.js](https://nuxtjs.org/)

Gatsby.js connaît un succès croissant (34000 ⭐ sur [github](https://github.com/gatsbyjs/gatsby)), c'est la technologie qui propulse la documentation de React, et c'est aussi une entreprise qui a levé 4 millions de dollars en mai 2018, preuve de l'intérêt de notre industrie pour les avantages offerts par cette solution et les solutions JAMStack en générale.

## Comment ça marche ?

Contrairement à un site web classique où chaque page est *recalculée à chaque visite* en interrogeant un serveur, qui lui-même interroge une base de données; **Gatsby génère toutes les pages à l'avance** en interrogeant les différents webservices fournisseurs de contenus et de données pour le site. 

Ces pages pré-générées sous formes de fichiers statiques HTML, JS et CSS sont spécialement optimisées pour offrir une performance maximale aux visiteurs. Il suffit ensuite placer ces fichiers statiques directement sur un "Content Delivery Network" (CDN) pour obtenir un site dont les pages sont servies de manières performantes et facilement scalable à l'échelle mondiale.

## Gatsby : un générateur de site statique nouvelle génération

Gatsby est techniquement un **générateur de site statique** basé sur l'interrogation de webservices pour obtenir contenus et données; et dont le html final est généré par des composants *React*. Ces données peuvent être récupérées de deux manières

- En utilisant l'API graphQL locale de Gatsby nourrie par l'installation de [sources plugins](https://www.gatsbyjs.org/plugins/). Installer un plugin [gatsby-source-wordpress](https://www.gatsbyjs.org/packages/gatsby-source-wordpress/?=wordpress) rendra par exemple automatiquement disponible dans l'API GraphQL locale les données d'un wordpress distant.

- Utiliser manuellement l'API `createPages` de Gatsby en scriptant soi-même les appels aux webservices (ou toute autre source de données)

Pour le visiteur, l'expérience est celle d'une **SPA (single page application)**, sans rechargement de page : bien que chacune des pages soient pré-générées en html par Gatsby, dès lors qu'on visite une page c'est bien *React* qui reprend entièrement la main en [*hydratant* le html](https://www.gatsbyjs.org/blog/2018-10-15-beyond-static-intro/#hydration). 

Puisqu'*in fine*, il s'agit d'une application React classique, cela signifie qu'il est aussi possible de créer des routes uniquement côté client, sans qu'elles soient pré-rendues en html, comme on le ferait pour une application React classique: https://www.gatsbyjs.org/docs/building-apps-with-gatsby/#client-only-routes--user-authentication


### Déployer et re-générer les pages d'un site Gatsby

La commmande `gatsby build` permet de compiler un site Gatsby dans un dossier `dist`. Il suffit de ensuite de déployer ce dossier compilé `dist` pour mettre le site en ligne. 

On peut confier cette tâche de compilation à serveur de build / un outil d'intégration continue qui pourra:

- Déclencher la re-compilation puis le déploiement en production du site lorsqu'un nouveau commit à lieu sur la branche `master`
- Exposer un *webhook* qui permettra déclencher la compilation et le déploiement du site à distance, quand un nouveau contenu est publié sur un CMS par exemple.

Il possible d'utiliser un service spécialisé tel que l'excellent [Netlify](https://www.netlify.com/) - spécialisé JAMStack - qui fait les choses ci-dessus avec une interface simple et claire, en offrant en prime d'autres fonctionnalités intéressantes comme:

- La possibilité de rollback en un clic vers une déploiement antérieur
- Les [branches de prévisualisations](https://www.netlify.com/blog/2016/07/20/introducing-deploy-previews-in-netlify/) 
- Le déploiement automatique de fonctions lambda chez AWS.
- bien d'autres choses pour épicer un site JAMStack que je vous laisse découvrir


### Quelques limites à Gatsby

- Gatsby n'est pas optimisé pour un site qui devrait générer un million de pages toutes les 5 minutes, le temps de construction augmente au fur et à mesure du nombres de pages. Une architecture JAMStack avec Gatsby est surtout adaptée pour le moment à des projets qui n'ont pas plus de quelques milliers ou quelques dizaines milliers de page [chiffres à vérifier] dont les contenus statiques ne changent pas en permanence.
- Il ne semble pas y avoir de solution officielle pour le multilingue, même si des astuces existent.




