## Partie 2 - Gestion de branches

_Cette partie est à faire sur le même dépôt que la partie précédente. C'est la suite._

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

- Faire un _commit_ intégrant cette ajout : "Ajout fichier5.md"

- Entrer la commande `git log --oneline --decorate --graph --all` pour visualiser, sur le terminal, le graphe des _commits_ sur toutes les branches

  - Noter la « déviation » entre les deux branches, à partir de la branche `master` (schématisée sous forme de traits)
  - l'option `--all` permet de visualiser toutes les branches, pas seulement celle sur laquelle on est
  - l'option `--oneline` affiche les _commits_ sur une seule ligne
  - l'option `--graph` affiche le log sous forme de graphe
  - (utilisez si besoin les touches haut/bas pour naviguer dans la sortie de cette commande et `Q` pour quitter)

- Installer l'extension VS Code _Git Graph_ et visualiser le graphe actuel des _commits_ à l'aide de cette extension
  - Sur cette représentation, que représente les points ?
  - Comment voit-on sur quelle branche on est actuellement ?
