## Partie 4 - Travailler avec un dépôt distant (_remote_)

- Faire un _fork_ du dépôt https://github.com/rose-line/sio1-2024-java-grpa (pas par commande Git, c'est sur l'interface GitHub)

- Cloner localement votre _fork_ (**ne pas cloner le dépôt original**)

  - Quelle est la différence entre un _fork_ et un clonage ?
  - Indiquer dans quelles circonstances on voudrait _forker_ et/ou cloner un dépôt

- Modifier le fichier `README.md` à la racine du dépôt en ajoutant une ligne quelconque

- On veut maintenant envoyer cette modification vers le dépôt distant

  - Il faut d'abord faire un _add/commit_ local
  - Puis utiliser la commande qui « pousse » les modifs sur le dépôt GitHub (_push_)
  - Vérifier directement sur GitHub que le _push_ a bien fonctionné

- Trouver la commande qui affiche le nom du ou des dépôt(s) distant(s) relié(s) avec le dépôt local : cela permet de savoir si le dépôt courant est synchronisé avec un dépôt en ligne ou non

- On va faire un _merge_ en local puis *push* :

  - Créer une branche locale `bugfix1`, se déplacer dessus, créer un nouveau fichier `ok.java` à la racine du dépôt
  - Ajouter `ok.java` à l'index et faire un _commit_
  - Retourner sur `master`, créer le fichier `ajout.java`, ajouter à l'index et committer
  - Fusionner la branche `bugfix1` dans la branche `master`
  - Afficher le log des *commits* ; noter les emplacements des trois branches différentes, en local et en remote
  - Faire un _push_
  - Refaire un affichage du log ; `origin/master` a bougé : que représente cette branche ?

- Étudier le résultat sur GitHub, en examinant _commits_ et branches (bouton _drop-down_ sur la page du dépôt pour voir les branches) : qu'est-ce qui est différent de la version locale ?

- Le bug est corrigé et intégré ; que doit-on faire de la branche `bugfix1` maintenant ?

- Supposons que l'on veuille effectivement publier sur le _remote_ une branche sur laquelle on travaille (pour sauvegarde ou pour que d'autres puissent l'utiliser)

  - Créer une nouvelle branche `partage`
  - Aller sur la branche
  - Ajouter un fichier `partage.md`
  - L'inclure dans l'index
  - Faire un _commit_
  - _Push_
  - Que se passe-t-il ?
  - Exécuter la bonne commande pour sauvegarder la branche sur le remote
  - Vérifier sur GitHub que la branche apparaît bien

- La branche `partage` n'a pas été fusionnée avant le *push* ; on va utiliser un autre moyen offert par GitHub pour fusionner une branche en *remote* : la **_Pull Request_**

  - La _Pull Request_ est très utilisée en collaboration : elle permet à l'intégrateur du projet d'examiner les demandes de _merge_ au niveau du _remote_ avant de les accepter (ou non)

- Sur GitHub, cliquer sur le bouton _Compare & pull request_, qui apparaît directement sur la page du dépôt depuis le dernier _push_ qui a ajouté la branche (voir ci-dessus).

- À gauche, la branche d'intégration (« *base* », qui reçoit le _merge_) ; à droite, la branche à fusionner (« *compare* »)

  - On doit fusionner `partage` dans `master`
  - Attention, il faut bien choisir le repo de base qui est sur votre propre compte (pas le compte du dépôt d'origine que vous avez _forké_)
  - On peut ajouter d'autres informations : titre et commentaire de la _pull request_, et même upload de fichiers annexes, liens éventuels... Également, on peut ajouter des labels pour étiquetter la _pull request_ et lui affecter un _reviewer_, qui va officiellement être en charge
  - Valider en cliquant sur le bouton _Create pull request_

- La page résultante informe sur les branches source et cible, sur les _commits_ concernés, les fichiers qui ont été modifiés...

- On peut aussi y démarrer une conversation notamment entre l'émetteur de la _pull request_ et l'intégrateur

- On voit que l'intégrateur (possesseur du compte cible) peut accepter la _pull request_ en cliquant sur le bouton _Merge pull request_ (ou refuser en cliquant sur _Close pull request_).

- En discutant de la _pull request_, on se rend compte que certaines choses devraient être modifiées

  - Repartir en local pour effectuer une modification sur `partage.md` et ajouter `precision.md`
  - _Commit_ des deux modifs
  - _Push_
  - Observer la *pull request* : que s'est-il passé ?
  - Finalement, faire le _merge_ sur la page de la _pull request_
  - Noter que l'interface nous propose alors de supprimer la branche devenue inutile ; supprimer la branche

- Dans un contexte de travail en collaboration sur un même dépôt, donner un _workflow_ (façon de travailler) possible qui va permettre à tous les intervenants de viser des ajouts à la branche d'intégration, d'en discuter, et ceci sans danger pour la branche d'intégration, avant que finalement l'intégrateur (probablement propriétaire du dépot) accepte les changements.
