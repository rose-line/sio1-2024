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
- On veut maintenant fusionner `fonctionnalite2` dans la branche d'intégration (`master`)
- Effectuer cette fusion
- Noter le changement dans l'onglet _Git Graph_. Que signifie la mention _Merge made by the ... strategy_ indiquée par la sortie de la commande ?
- Quelle est la différence fondamentale avec la fusion précédente ?
- Créer une nouvelle branche `fonctionnalite3`, se déplacer dessus, et modifier le fichier `fichier1.md` en y ajoutant une ligne de texte. Committer : "Modification fichier1 pour fonctionnalité 3"
  - Comment utiliser _Git Graph_ pour qu'il nous montre les différences entre l'ancienne version de `fichier1.md` et la version courante que l'on vient de committer ?
- Repartir sur `master`, et modifier `fichier1.md` en y ajoutant aussi une ligne (différente de celle qu'on a ajoutée sur l'autre branche)
- Ajouter à l'index et faire un commit
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

### Travailler avec un hébergeur Git distant

- Faire un _fork_ du dépôt https://github.com/rose-line/sio1-2024-java-grpa (pas par commande Git, c'est sur l'interface GitHub)
- Cloner localement votre _fork_ (ne pas cloner le dépôt original)
  - Quelle est la différence entre un _fork_ et un clonage ?
  - Indiquer dans quelles circonstances on voudrait _forker_ et/ou cloner un dépôt
- Modifier le fichier `README.md` à la racine du dépôt en ajoutant une ligne quelconque
- On veut maintenant envoyer cette modification vers le dépôt distant
  - Il faut d'abord faire un add/commit local
  - Puis utiliser la commande qui « pousse » les modifs sur le dépôt GitHub (_push_)
  - Vérifier directement sur GitHub que le _push_ a bien fonctionné
- Trouver la commande qui affiche le nom du ou des dépôt(s) distant(s) relié(s) avec le dépôt local : cela permet de savoir si le dépôt courant est synchronisé avec un dépôt en ligne ou non
- _Merge_ en local puis push :
  - Créer une branche locale `bugfix1`, se déplacer dessus, créer un nouveau fichier `ok.java` à la racine du dépôt
  - Ajouter `ok.java` à l'index et faire un commit
  - Retourner sur `master`, créer le fichier `ajout.java`, ajouter à l'index et commit
  - Fusionner la branche `bugfix1` dans la branche `master`
  - Afficher le log des commits ; noter les emplacements des trois branches différentes, en local et en remote
  - Faire un _push_
  - Refarire un affichage du log ; `origin/master` a bougé : que représente cette branche ?
- Étudier le résultat sur GitHub, en examinant commits et branches (bouton _drop-down_ sur la page du dépôt pour voir les branches) : qu'est-ce qui est différent de la version locale ?
- Le bug est corrigé et intégré ; que doit-on faire de la branche `bugfix1` maintenant ?
- Supposons que l'on veuille effectivement publier sur le _remote_ une branche sur laquelle on travaille (pour sauvegarde ou pour que d'autres puissent l'utiliser)
  - Créer une nouvelle branche `partage`
  - Aller sur la branche
  - Ajouter un fichier `partage.md`
  - L'inclure dans l'index
  - Faire un commit
  - _Push_
  - Que se passe-t-il ?
  - Exécuter la bonne commande pour sauvegarder la branche sur le remote
  - Vérifier sur GitHub que la branche apparaît bien
- La branche `partage` n'a pas été fusionnée avant le *push* ; on va utiliser un autre moyen offert par GitHub pour fusionner une branche en *remote* : la **_Pull Request_**
  - La _Pull Request_ est très utilisée en collaboration : elle permet à l'intégrateur du projet d'examiner les demandes de _merge_ au niveau du _remote_ avant de les accepter (ou non)
- Sur GitHub, cliquer sur _Pull Request_
- À gauche, la branche d'intégration (« *base* », qui reçoit le _merge_) ; à droite, la branche à fusionner (« *compare* »)
  - On doit fusionner `^partage` dans `master`
  - Si, avant, GitHub vous demande de choisir un repo de base, bien prendre celui qui est sur votre propre compte
- Cliquer sur _Create Pull Request_
- Le nouveau formulaire vous permet d'ajouter des informations : titre et commentaire de la _pull request_, et même upload de fichiers annexes, liens éventuels... Également, on peut ajouter des labels pour étiquetter la _pull request_ et lui affecter un _reviewer_, qui va officiellement être en charge
  - Valider
  - La page résultante informe sur les branches source et cible, sur les commits concernés, les fichiers qui ont été modifiés...
  - On peut aussi y démarrer une conversation notamment entre l'émetteur de la _pull request_ et l'intégrateur
- En discutant de la _pull request_, on se rend compte que certaines choses devraient être modifiées
  - Repartir en local pour effectuer une modification sur `partage.md` et ajouter `precision.md`
  - Commit des deux modifs
  - _Push_
  - Observer la *pull request* : que s'est-il passé ?
  - Finalement, faire le _merge_ sur la page de la _pull request_
  - Noter que l'interface nous propose alors de supprimer la branche devenue inutile ; supprimer la branche
- Dans un contexte de travail en collaboration sur un même dépôt, donner un _workflow_ (façon de travailler) possible qui va permettre à tous les intervenants de viser des ajouts à la branche d'intégration, d'en discuter, et ceci sans danger pour la branche d'intégration, avant que finalement l'intégrateur (probablement propriétaire du dépot) accepte les changements

### Travailler en collaboration sur GitHub

Cette partie est plus intéressante avec en binôme, mais on peut également simuler les interactions sur un seul poste.

#### Setup

- L'un joue Jean-Michel, l'autre Sylvie-Arnaude (si vous êtes seul, vous jouez les deux rôles)
- _(pour binômes uniquement)_ Jean-Michel doit ajouter Sylvie-Arnaude en tant que collaboratrice de son dépôt de travail :
  - se rendre dans les _settings_ du dépôt / _Manage Access_ / _Invite a collaborator_
  - trouver et ajouter le compte de Sylvie-Arnaude
  - à présent chacun peut _push_ des branches et des commits sur le dépôt
- Sylvie-Arnaude se place dans son répertoire de projets général (qui contient les répertoires de tous ses projets) et clone le dépôt de Jean-Michel (vous ajouterez en paramètre de la commande `clone` le nom du répertoire de destination : `tp-git-sa`)
- Jean-Michel est censé déjà avoir le même projet en local, mais il va également cloner une nouvelle copie appelée `tp-git-jm` (attention de ne pas être dans le répertoire du dépôt existant au moment de taper la commande)

#### Travail collaboratif sur le même dépôt

- Sylvie-Arnaude va effectuer quelques modifications sur sa copie du dépôt :
  - Créer une branche (basée sur `master`) appelée `sa-modif` (bonne pratique : faire un `git status` pour vérifier que le dépôt est _clean_ et vérifier qu'on est sur la bonne branche de base avant de créer la nouvelle branche)
  - Créer un fichier `sa-fichier1.md` avec du contenu
  - Indexer et faire un commit de cet ajout : `"premier commit de Sylvie-Arnaude"`
- On va rendre ce travail local disponibe sur le _remote_
  - On sait qu'on a deux moyens principaux de faire ça :
    1. Fusionner localement puis _push_
    2. _Push_ directement puis créer une _Pull Request_
  - On va utiliser la première option ici (on se rappelle que, si on travaille en équipe, on doit établir une convention commune pour ce genre de choix)
    - Faire un _merge_ de `sa-modif` dans `master` (attention : pour une fusion, il faut être sûr d'être sur la branche `master` avant d'initier le _merge_)
    - cela crée-t-il un nouveau commit ou non et pourquoi ?
    - Maintenant, on _push_ la branche `master`
    - On peut finalement supprimer la branche `sa-modif`
- À ce stade, Jean-Michel a son dépôt local qui est « un commit en retard » par rapport au dépôt distant : il ne « voit » pas les modifications faites par Sylvie-Arnaude
- Mais pour l'instant, Sylvie-Arnaude continue à travailler localement :
  - elle liste les branches courantes (normalement une seule) en utilisant le paramètre `-vv` (_very verbose_) de la commande `git branch`
  - elle crée une nouvelle branche `sa-fonctionnalite` basée sur `master` et _switch_ dessus
  - elle modifie le fichier `sa-fichier1.md`
  - elle indexe la modification et commit
  - elle liste de nouveau les branches en _very verbose_ et note que la nouvelle branche ne possède pas d'équivalent sur le _remote_
  - elle _push_ en créant la nouvelle branche sur le _remote_
  - elle liste encore les branches et note le pointeur `origin/sa-fonctionnalite` qui a été créé ; il y a donc trois branches qui permettent de gérer `sa-fonctionnalite` :
    - la branche locale `sa-fonctionnalite`
    - la branche _ramote_ `sa-fonctionnalite`
    - la branche de _tracking_ `origin/sa-fonctionnalite` qui permet à Git de relier les deux autres branches ; on ne peut pas manipuler directement cette branche, mais Git s'en sert pour la sunchronisation ; quand on _push_ depuis la branche `sa-fonctionnalite`, les trois branches pointent sur le même commit
- À ce stade, Jean-Michel a deux commits de retard en local (mais un seul par rapport à _master_) et ne connaît pas non plus la branche `sa-fonctionnalite`
- Jean-Michel commence maintenant à travailler :
  - il liste les branches en _very verbose_
  - il crée une branche `jm-fonctionnalite` et s'y déplace
  - il crée un nouveau fichier `jm-fichier1.md`
  - il l'indexe et commit
  - il liste les branches et note et note que la nouvelle branche n'a pas de branche de _tracking_ associée, et donc pas de _remote branch_
  - il _push_ en créant la branche de _tracking_
  - il liste de nouveau les branches et note que la _tracking branch_ existe
- Combien y a-t-il de branches (en incluant les branches de _tracking_) sur le dépôt local de Jean-Michel ?
- Combien y a-t-il de branches sur le *remote* ?
- Les branches `jm-fonctionnalite`, `origin/jm-fonctionnalite` et la branche _remote_ `jm-fonctionnalite` pointent toutes vers le même commit : vrai ou faux ?
- Le clone de Sylvie-Arnaude connaît-il la branche `jm-fonctionnalite` ?
- Jean-Michel fait un _pull_ pour récupérer le travail de Sylvie-Arnaude
- Sylvie-Arnaude fait de même pour récupérer le travail de Jean-Michel
- Souvenez-vous que la commande _pull_ fait deux choses :
  - récupérer (_fetch_) les nouveaux commits et les nouvelles branches depuis le _remote_
  - fusionner (_merge_) ces modifications localement : cela peut potentiellement provoquer des conflits, comme nous l'avons vu précédemment ; ceux-ci seront résolus manuellement de la même manière
- Simulez du travail sur les deux clones dans le but de provoquer un conflit au moment du _pull_ chez Sylvie-Arnaude
  - Résolvez les conflits localement
  - Utilisez une _Pull Request_ pour proposer la résolution en _remote_
