# Architecture web JAMStack avec React et Gastby.js : SEO, rapidité, sécurité, scalabibilité

JAMStack est une architecture web conçue pour offrir au visiteur une expérience ultra-rapide sur tous les appareils, obtenir  d'excellents résultats en SEO et pour alléger au maximum la charge de travail technique liée à la scalabilité et maintenance du serveur et de la base de donnée d'un site web.

Mais ce n'est pas tout, un architecture JAMStack permet également :

- Une prévisualisation complète du site avant publication définitive des nouveaux contenus.
- De revenir en un clic à la version précédente du site 
- De faire du "A/B" testing en faisant atterir les visiteurs tantôt sur l'une ou l'autre version du site
- de réduire drastiquement voir d'éliminer les risques de piratages et les failles de sécurité
- De réduire les coûts de maintenances côté serveur
- De détecter des erreurs dans le site avant la mise en production, lors de la phase de "compilation" du site
- Une très grande facilité à changer de prestataire d'hébergement si nécessaire : ce sont techniquement juste des fichiers statiques à uploader ailleurs en quelques minutes.

## Architecture JAMStack avec React

**React n'est pas SEO-friendly**. Aujourd'hui, les contenus des sites codés en React ne sont pas visibles par les moteurs de recherches dès lors qu'il y a plusieurs pages gérées par un *routeur* (un test de visite avec *google search console* affiche une page vide). 

Une manière de transformer ce problème en atout majeur pour un projet est d'utiliser [**Gatsby**](https://www.gatsbyjs.org/): il permet de créer un site JAMStack avec React. Gatsby JS connaît un succès croissant et est également une entreprise qui a lever 3,8 millions de dollars En mai 2018; preuve de l'intérêt du secteur pour les avantages offerts par ce type d'architecture.

## Techniquement, comment ça marche ?

### les "Néo-GSS"

Gatsby fait partie d'une nouvelle génération de **générateur de site statique** (GSS), basé sur l'interrogation d'APIs et dont le html est généré à partir de librairies front-end modernes telles que React. *Gatbsy* (ou *Gridsome* côté Vue.js) sont en quelques sorte les enfants prodiges de *Jekyll*, et il n'y a plus grand chose de "statique" dans un site généré par Gatsby; c'est désormais plutôt une autre approche pour créer un site dynamique, en déportant l'intelligence d'un serveur monolitique vers des webservices et un front en JavaScript. 

Le résultat est une "SPA" (single page application) : bien que toutes les pages soient prégénérées en html, dès qu'on visite une page c'est bien React qui prend entièrement la main en "hydratant" le html, offrant ainsi une expérience en temps réel à l'utilisateur, tout comme une application React classique.

### Compilation versus interprétation

Contrairement à un site web classique où chaque page est *recalculée à chaque visite* en interrogeant un serveur qui lui même interroge une base de données, **Gatsby génère toutes les pages à l'avance** en interrogeant des API pour récupérer les contenus, les produits, les utilisateurs etc. 

Cette phase de "compilation" du site permet de nombreuses optimisations (poids des images, poids et chargements des CSS, JS) pour permettre le chargement le plus rapide possible de la page. Gatsby offre notamment par défaut un chargement intelligent et paresseux de chaque image, et prégénère au moment de la compilation les différentes tailles d'images pour optimiser leur vitesse d'affichage, en afficheant une version "floue" et légère de l'image pendant son chargement.

Le résultat ce cette pré-compilation est un ensemble de fichier html, CSS, et JavaScript qu'il suffit de déployer sur n'importe quel "CDN" pour obtenir des performances excellentes à une échelle mondiale et une scalabilité sans faille et sans efforts. 

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



