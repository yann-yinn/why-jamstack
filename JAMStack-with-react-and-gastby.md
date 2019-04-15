# Avantages d'une Architecture : SEO, rapidité, sécurité, scalabilité, sérénité

JAMStack est une architecture web conçue pour offrir au visiteur une expérience ultra-rapide sur tous les appareils, obtenir  d'excellents résultats en SEO et pour alléger la charge de travail technique liée à la scalabilité du serveur et de la base de donnée d'un site web. Une architecture JAMStack permet également une réduction drastique voire une suppression totale des risques de piratage et des failles de sécurité.

On peut citer parmi les autres avantantages: 

- Préchargement des autres pages pendant la visite d'une page
- Pouvoir revenir en un clic à la version précédente du site
- Pouvoir faire du "A/B" testing en faisant atterir les visiteurs tantôt sur l'une ou l'autre version du site
- Avoir une prévisualisation complète du site avant publication définitive des nouveaux contenus.
- Détecter des erreurs dans le site avant la mise en production, grâce à la phase de "compilation" du site
- Une très grande facilité à changer de prestataire d'hébergement si nécessaire : ce sont techniquement juste des fichiers statiques à uploader ailleurs en quelques minutes.

![](https://raw.githubusercontent.com/yann-yinn/why-jamstack/master/images/ligthouse.png?token=AAUeh8-GslHUXclNnzgWHf32Z1d15ELqks5cvZ2lwA%3D%3D)
> Ci-dessus le résultat d'un audit [lighthouse](https://developers.google.com/web/tools/lighthouse) sur le site https://popcorn-nantes.github.io basé sur une architecture JAMStack

## Architecture JAMStack avec React

**React n'est pas SEO-friendly**. Aujourd'hui, les contenus des sites codés en React ne sont pas visibles par les moteurs de recherches dès lors qu'il y a plusieurs pages gérées par un *routeur* (un test de visite avec *google search console* affiche une page vide). 

Une manière de transformer ce problème en atout majeur pour un projet est d'utiliser [**Gatsby**](https://www.gatsbyjs.org/): il permet de créer un site JAMStack avec React. Gatsby JS connaît un succès croissant et est également une entreprise qui a levé 3,8 millions de dollars En mai 2018; preuve de l'intérêt du secteur pour les avantages offerts par ce type d'architecture.

## Comment ça marche ?

Contrairement à un site web classique où chaque page est *recalculée à chaque visite* en interrogeant un serveur qui lui-même interroge une ou plusieurs base(s) de données (obligeant en général la mise en place d'une infrastructure dédiée à la gestion du cache), **Gatsby génère toutes les pages à l'avance** en interrogeant les différents webservices fournisseurs de contenus et de données pour le site. Ces pages pré-générées sont spécialement optimisées pour offrir une performance maximale aux visiteurs. Il suffit ensuite placer ces pages pré-générées directement sur un "Content Delivery Network" (CDN) pour obtenir un site dont les pages sont servies de manières utra-performantes à l'échelle mondiale.

### Considérations techniques sur Gatsby, un "Néo-GSS" 

Gatsby fait partie d'une nouvelle génération de **générateur de site statique** (GSS), basé sur l'interrogation d'APIs et dont le html est généré à partir de librairies front-end modernes telles que React. 

*Gatbsy* (ou *Gridsome* côté Vue.js) sont en quelques sorte les enfants prodiges de *Jekyll* (moteur de blog statique basé sur des fichiers markdowns), et il n'y a pas grand chose de "statique" dans un site généré par Gatsby; c'est plutôt une autre approche pour créer un site dynamique, en déportant l'intelligence d'un serveur monolitique vers des webservices et la génération dynamique du html côté JavaScript (client) pluôt que côté serveur.

Le résultat produit par Gatsby est une "SPA" (single page application) : bien que toutes les pages soient prégénérées en html, dès qu'on visite une page c'est bien React qui reprend entièrement la main en "hydratant" le html, offrant ainsi une expérience en temps réel à l'utilisateur, identique à une application React classique mais avec en primer des données "pré-chargées" lors de la phase de compilation pour accélérer la navigation.

### Compilation versus interprétation

Contrairement à un site web classique où chaque page est *recalculée à chaque visite* en interrogeant un serveur qui lui même interroge une base de données, **Gatsby génère toutes les pages à l'avance** en interrogeant des API pour récupérer les contenus, les produits, les utilisateurs etc. 

Cette phase de "compilation" du site permet de nombreuses optimisations (poids des images, poids et chargements des CSS, JS) pour permettre le chargement le plus rapide possible de la page. Gatsby offre notamment par défaut un chargement intelligent et paresseux de chaque image, et prégénère au moment de la compilation les différentes tailles d'images pour optimiser leur vitesse d'affichage, en afficheant une version "floue" et légère de l'image pendant son chargement.

Le résultat ce cette pré-compilation est un ensemble de fichier Html, CSS, et JavaScript qu'il suffit de déployer sur n'importe quel "CDN" pour obtenir des performances excellentes à une échelle mondiale et une scalabilité sans faille et sans efforts. 

### déclencher la génération des pages

A chaque changement d'un article, d'un produit, il faut "reconstruire" le site en entier pour "publier" les changements. Pour rendre cela transparent pour les rédacteurs et rédactrices de contenus, il est suffit de "pinguer" une url qui déclenchera la re-génération du site (un webhook) sur le serveur dédié au "build" du site. 

Cela peut prendre quelques minutes mais les temps sont généralement très raisonnables et cela offre une contre-partie non-négligeable : les déploiement deviennent **atomique** : ça signifie que ce système permet de revenir à la version précédente du site, contenus compris, simplement en revenant à la version précédente des fichiers; ce qui devient aisé en stockant les fichiers du build sur un repo git. 

Mieux, puisque le site est désormais sous forme de "snapshots" (les différentes builds qui ont été faits), il devient facile de mettre en place des fonctionnalités habituellement complexes en jouant sur les branches pour tester une version ou une autre du site, prévisualiser le build sur une branche à part avant publication sur le master etc... 

## Hébergeurs spécialisés JAMStack

A noter qu'il existe de plus en plus d'hébergeurs pour faciliter les déploiements d'un site JAMStack. A partir d'un dépôt Git, *Netlify* permet par exemple de générer son site à chaque push, de rédéclencher un build par ping d'une URL, d'avoir une interface de rollback, des logs détaillés, d'avoir des branches de prévisualisation, l'A/B testing etc

Netlify permet auss d'uploader un dossier contenant des fonctions lambdas et les déploit lui même automatiquement sur AWS !

## Les limites de JAMStack

- Gatsby n'est pas optimisé pour un site qui devrait générer un million de pages toutes les 5 minutes... Cette solution convient donc mieux à des sites qui ont de quelques pages à quelques milliers de page, le temps de génération du site étant proportionnel aux nombres de pages et aux appels aux APIs à effectuer.

## Conclusion

Comme tout en informatique, il s'agit d'un compromis entre différents objectifs. JAMStack est une architecture qui se concentre avant tout sur une réduction du temps de travail et des coûts concernant les problématiques de SEO, de performances, de sécurité et de scalabibilité. **Gatsby** est de son côté solution JAMStack très populaire et en pleine croissante, qui permet en outre d'avoir toute la puissance de React côté front-end.



