# Cahier des charges

## Définition du besoin

### Définition

Le suivi des frais est actuellement géré de plusieurs façons selon le laboratoire d'origine des visiteurs. On souhaite uniformiser cette gestion. L'application doit permettre d'enregistrer tout frais engagé, aussi bien pour l'activité directe (déplacement, restauration et hébergement) que pour les activités annexes (événementiel, conférences, autres), et de présenter un suivi daté des opérations menées par le service comptable (réception des pièces, validation de la demande de remboursement, mise en paiement, remboursement effectué).

### Forme

L'application destinée aux visiteurs, délégués et responsables de secteur sera accessible depuis un ordinateur, tout comme la partie utilisée par les services comptables.

## Contraintes

### Environnement technique

- Langage et écosystème : Java
- Interface graphique de type « bureau » : JavaFX
- Système de Gestion de bases de données : MySQL
- Interface entre le code Java et le SGBDR : JDBC
- Toute autre bibliothèque (internes ou externes au JDK) que vous jugerez nécessaires, du moment que c'est justifié

### Modules

L'application présente deux modules :

- Module 1 : enregistrement et suivi par les visiteurs
- Module 2 : enregistrement des opérations par les comptables

### Documentation

La documentation devra présenter :

- l'arborescence des écrans pour chaque module
- le descriptif des éléments, classes et bibliothèques utilisées
- le schéma entités-associations et le schéma relationnel correspondant (on pourra utiliser [MoCoDo](http://www.mocodo.net/) pour créer une version numérique, une fois que le schéma sera supposé complet)
- un jeu de données de test permettant d'illustrer l'ensemble des fonctionnalités de l'application (il pourra être partiellement généré par un outil, par exemple [GenerateData](http://www.generatedata.com))
- la liste des frameworks et/ou bibliothèques externes utilisés
- la liste des divers outils de gestion de projet utilisés

### Responsabilités

Le commanditaire fournira à la demande toute information sur le contexte nécessaire à la production de l'application. Les demandes se feront sous la forme d'un ticket sur ce dépôt Github (voir onglet _Issues_).

Le prestataire est à l'initiative de toute proposition technique complémentaire.

Le prestataire fournira un système opérationnel, une documentation technique permettant un transfert de compétence et un mode opératoire propre à chaque module.
