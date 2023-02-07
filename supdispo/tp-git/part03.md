## Partie 3 - Fusionner des branches

_Cette partie est à faire sur le même dépôt que la partie précédente. C'est la suite._

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

- Repartir sur `master`, et modifier `fichier1.md` en y ajoutant aussi une ligne (différente de celle qu'on a ajoutée sur l'autre branche) ; ajouter à l'index et _commit_

- Tenter de fusionner la branche `fonctionnalite3` avec `master`

  - Que se passe-t-il et pourquoi ?

- Lancer un `git status`

  - Que doit-on faire si on veut annuler la fusion en cours ? (**ne pas lancer la commande**)

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

  - Il ne doit plus y avoir de marques quelconques en dehors des ajouts fonctionnels originaux, c'est-à-dire pas de `<<<<<<<<<<`, ni de mentions de nom de branche, etc. : vous rendez le fichier tel qu'il doit apparaître dans le _commit_ de fusion, avec les conflits résolus manuellement
  - Sauvegarder

- Ajouter les modification à l'index et committer

- NB : parfois, plusieurs fichiers sont en conflit ; le processus est identique, il faut juste résoudre les conflits sur tous les fichiers

- NB : les conflits de fusion sont fréquents lorsqu'on travaille en collaboration (plusieurs personnes vont travailler sur le même fichier pour remplir deux fonctionnalités différentes)

- Les branches créées n'ont plus de raison d'exister

  - Elles avaient pour but de créer une déviation afin de travailler sur des fonctionnalités individuelles, sans interférer avec le travail des autres, avant de les fusionner dans la branche d'intégration
  - On va vouloir nettoyer le dépôt en les supprimant
  - Cela ne va bien sûr pas supprimer tous les _commits_ qui y sont associés
  - Attention cependant d'éviter en général de supprimer une branche qui n'a pas encore été intégrée à la branche d'intégration, sauf on souhaite vraiment abandonner le développement de cette branche
  - Ne pas réutiliser une branche qui a déjà été intégrée pour démarrer une nouvelle piste : toujours utiliser une nouvelle branche
  - Nouvelle tâche ? => nouvelle branche à partir d'un _commit_ de la branche d'intégration (en général le plus récent)
  - Tâche terminée ? => fusion dans la branche d'intégration et suppression de la branche

- Supprimer les trois branches `fonctionnalitex` (attention : on ne peut pas supprimer une branche sur laquelle on est)
