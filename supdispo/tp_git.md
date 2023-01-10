# TP Utilisation de Git en CLI

## Introduction

Le TP est à effectuer entièrement en ligne de commande (CLI = _Commnand Line Interface_), sauf utilisation annexe de VS Code, notamment pour éditer des fichiers.

Le rendu va consister à fournir au professeur votre dépôt de travail, que vous devrez créer lors du TP. Ce dépôt contiendra le résultat des commandes du TP, ainsi qu'un fichier-réponse. Pour cela, voici la procédure à suivre :

- Copiez la partie « Travail à faire » dans un fichier local
- **Ajoutez votre nom en tout début de fichier.**
- Écrivez la totalité des commandes que vous effectuez, au fur et à mesure, _juste en dessous_ de chacune des étapes
- De même pour les réponses aux questions spécifiques
- Le fichier-réponse ainsi constitué devra être placé dans votre dépôt de travail, avec tous les autres fichiers que vous aurez créés pour le TP.
- Ce dépôt devra être hébergé sur GitHub (utilisez VS Code pour publier le dépôt automatiquement)
- Vous ajouterez le compte GitHub `rose-line` en tant que collaborateur : cela enverra automatiquement une notification sur le compte en question
- Vous committerez vos réponses au fur et à mesure, quand vous le souhaitez, sans oublier de « pousser » (_push_) vos modifications en ligne à la fin de la séance

Prérequis :

- Visual Studio Code
- Git installé sur le système (_Git Bash_ est normalement également installé)
- Configuration de base (`user.name` et `user.email`)
- Faire de VS Code l'éditeur de texte par défaut utilisé par les commandes Git si besoin :
  - `git config --global editor.core "code -w"`

Annexe :

[Résumé des commandes Git les plus utilisées](commandes_git.md)

## Travail à faire

- Ouvrir un terminal (terminal _Git Bash_ à privilégier)
- Créer, en ligne de commande, un répertoire `tp-git`
- Se déplacer dans le répertoire
- Vérifier qu'on est dans le bon répertoire en affichant le chemin du répertoire courant
- Initialiser un dépôt Git
- Lister tous les fichiers du répertoire (y compris les fichiers cachés) pour s'assurer que le répertoire `.git` à été créé
- Ouvrir ce répertoire sous VS Code
- Exécuter `git status` et copier/coller la sortie
- Créer le fichier `fichier1.md` avec un contenu quelconque et l'enregistrer
- Créer le fichier `fichier2.md` avec un contenu quelconque et l'enregistrer
- Exécuter `git status` et copier/coller la sortie
- Ajouter `fichier1.md` à l'index de Git (zone de _Staging_)
- Exécuter `git status` et copier/coller la sortie
- Créer un commit avec pour message : "Ajout de fichier1.md"
- Exécuter `git status` et copier/coller la sortie
- Modifier `fichier1.md` et enregistrer
- Exécuter `git status` et copier/coller la sortie
- Ajouter `fichier1.md` et `fichier2.md` à la zone de _Staging_
- Créer un commit "Ajout de fichier2.md et modification de fichier1.md"
- Copier/coller l'ID des deux premiers commits :
  - ID commit 1 :
  - ID commit 2 :
- Que signifie qu'un fichier est "_tracked_" ou "_untracked_" ?
- Pourquoi doit-on passer les fichiers par la zone de _Staging_ (l'index) avant de les committer ?
- Créer une branche `fonctionnalite1`
- Lister les branches
- Se déplacer sur la branche `fonctionnalite1`
- Lister les branches
- Que représente l'étoile à côté des noms des branches ?
- Créer un nouveau fichier `fichier3.md`
- Modifier le fichier `fichier2.md`
  - Comment utiliser VS Code pour qu'il nous montre les différences entre l'ancienne version de `fichier2.md` et la version courante que l'on vient d'éditer ?
- Committer ces deux modifications : "Fonctionnalité 1 - première phase"
- Créer un nouveau fichier `fichier4.md`
- Modifier de nouveau le fichier `fichier2.md`
- Committer ces deux modifications : "Fonctionnalité 1 - terminée"
- Afficher la liste des fichiers du répertoire
- Se déplacer sur la branche `master`
- Afficher la liste des fichiers du répertoire
- Pourquoi les deux sorties sont-elles différentes ? Les fichiers ont-ils disparus ?
- Créer une nouvelle branche `fonctionnalite2`
  - Cette branche ne va pas avoir toutes les données incluses dans `fonctionnalite1`. Pourquoi ?
  - Qu'aurait-il fallu faire si on avait souhaité démarrer la branche `fonctionnalite2` en intégrant les modifications récentes de `fonctionnalite1` ?
- Se déplacer sur la nouvelle branche `fonctionnalite2`
- Créer un nouveau fichier `fichier5.md`
- Faire un commit intégrant cette ajout : "Ajout fichier5.md"
- Entrer la commande `git log --oneline --decorate --graph --all` pour visualiser, sur le terminal, le graphe des commits sur toutes les branches
  - Noter la « déviation » entre les deux branches, à partir de la branche `master`
- Installer l'extension VS Code _Git Graph_ et visualiser le graphe actuel des commits à l'aide de cette extension
  - Sur cette représentation, que représente les points ?
  - Comment voit-on sur quelle branche on est actuellement ?
- On considère que la branche originale (`master` ou `main`) est la branche d'intégration, c'est-à-dire celle qui va contenir l'historique de toutes les modifications développées au fur et à mesure dans les branches annexes
- On va maintenant fusionner la branche `fonctionnalite1`, qui est terminée, avec la branche d'intégration
- Se déplacer sur la branche `master`
  - Noter le changement dans l'onglet _Git Graph_
- Fusionner avec la branche `fonctionnalite1`
- Noter le changement dans l'onglet _Git Graph_. Que signifie la mention _Fast-forward_ indiquée par la sortie de la commande ?
-
- On veut maintenant fusionner `fonctionnalite2` dans la branche d'intégration (`master`)
- Effectuer cette fusion
- Noter le changement dans l'onglet _Git Graph_. Que signifie la mention _Merge made by the ... strategy_ indiquée par la sortie de la commande ?
- Quelle est la différence fondamentale avec la fusion précédente ?
- Créer une nouvelle branche `fonctionnalite3`, se déplacer dessus, et modifier le fichier `fichier1.md` en y ajoutant une ligne de texte. Committer : "Modification fichier1 pour fonctionnalité 3"
  - Comment utiliser _Git Graph_ pour qu'il nous montre les différences entre l'ancienne version de `fichier1.md` et la version courante que l'on vient de committer ?
- Repartir sur `master`, et modifier `fichier1.md` en y ajoutant aussi une ligne (différente de celle qu'on a ajoutée sur l'autre branche)
- Tenter de fusionner la branche `fonctionnalite3` avec `master`
  - Que se passe-t-il et pourquoi ?
- Lancer un `git status`
  - Que doit-on faire si on veut annuler la fusion en cours ?
- On veut résoudre le conflit. Plusieurs possibilités :
  - Conserver uniquement les modifications faites dans `fonctionnalite3`
  - Conserver uniquement les modifications faites dans `master`
  - Conserver les deux modifications
  - Supprimer les deux modifications ou remanier sensiblement le fichier pour les intégrer correctement
- Git nous laisse totalement la main et ne va pas essayer d'imposer l'un de ces choix pour nous, ni nous assister dans l'application automatique de l'un d'entre eux : il faut examiner le(s) fichier(s) en conflit et éditer nous-mêmes
- Ouvrir le fichier en question sous VS Code
  - La chaîne `<<<<<<<<<<` marque le début du conflit
  - La chaîne `>>>>>>>>>>` marque la fin du conflit
  - La chaîne `==========` sépare les deux versions
- Éditer le fichier pour faire en sorte d'intégrer les deux modifications ; à la fin de l'édition :
  - Sauvegarder
  - Il ne doit plus y avoir de marques quelconques en dehors des ajouts fonctionnels originaux, c'est-à-dire pas de `<<<<<<<<<<`, ni de mentions de nom de branche, etc. : vous rendez le fichier tel qu'il doit apparaître dans le commit de fusion, avec les conflits résolus manuellement
- Ajouter les modification à l'index et committer
- NB : parfois, plusieurs fichiers sont en conflit ; le processus est identique, il faut juste résoudre les conflits sur tous les fichiers
- NB : les conflits de fusion sont fréquents lorsqu'on travaille en collaboration (plusieurs personnes vont travailler sur le même fichier pour remplir deux fonctionnalités différentes)
- Les branches créées n'ont plus de raison d'exister
  - Elles avaient pour but de créer une déviation afin de travailler sur des fonctionnalités individuelles
  - On va vouloir nettoyer le dépôt en les supprimant
  - Cela ne va bien sûr pas supprimer tous les commits qui y sont associés
  - Attention cependant d'éviter en général de supprimer une branche qui n'a pas encore été intégrée à la branche d'intégration, sauf on souhaite vraiment abandonner le développement de cette branche
  - Ne pas réutiliser une branche qui a déjà été intégrée pour démarrer une nouvelle piste : toujours utiliser une nouvelle branche
  - Nouvelle tâche ? => nouvelle branche à partir d'un commit de la branche d'intégration (en général le plus récent)
  - Tâche terminée ? => fusion dans la branche d'intégration et suppression de la branche
- Supprimer les trois branches `fonctionnalitex` (attention : on ne peut pas supprimer une branche sur laquelle on est)
