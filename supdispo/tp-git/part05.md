## Partie 5- Travailler en collaboration avec GitHub

Cette partie est plus intéressante avec un binôme, mais on peut également simuler les interactions sur un seul poste. On va simuler un travail collaboratif sur un même dépôt avec deux collaborateurs : Jean-Michel et Sylvie-Arnaude.

### Mise en place

- L'un joue Jean-Michel, l'autre Sylvie-Arnaude (si vous êtes seul, vous jouez les deux rôles)

- _(pour binômes uniquement)_ Jean-Michel doit ajouter Sylvie-Arnaude en tant que collaboratrice de son dépôt de travail :

  - se rendre dans les _settings_ du dépôt / _Manage Access_ / _Invite a collaborator_
  - trouver et ajouter le compte de Sylvie-Arnaude
  - à présent chacun peut _push_ des branches et des _commits_ sur le dépôt

- Sylvie-Arnaude se place dans son répertoire de projets général (qui contient les répertoires de tous ses projets) et clone le dépôt de Jean-Michel (vous ajouterez en paramètre de la commande `clone` le nom du répertoire de destination : `tp-git-sa`)

- Jean-Michel est censé déjà avoir le même projet en local, mais il va également cloner une nouvelle copie appelée `tp-git-jm` (attention de ne pas être dans le répertoire du dépôt existant au moment de taper la commande)

### Travail collaboratif sur le même dépôt

- Sylvie-Arnaude va effectuer quelques modifications sur sa copie du dépôt :

  - Créer une branche (basée sur `master`) appelée `sa-modif` (bonne pratique : faire un `git status` pour vérifier que le dépôt est _clean_ et vérifier qu'on est sur la bonne branche de base avant de créer la nouvelle branche)
  - Créer un fichier `sa-fichier1.md` avec du contenu
  - Indexer et faire un _commit_ de cet ajout : `"premier commit de Sylvie-Arnaude"`

- On va rendre ce travail local disponible sur le _remote_

  - On sait qu'on a deux moyens principaux de faire ça :
    1. Fusionner localement puis _push_
    2. _Push_ directement puis créer une _Pull Request_
  - On va utiliser la première option ici (on se rappelle que, si on travaille en équipe, on doit établir une convention commune pour ce genre de choix)
    - Faire un _merge_ de `sa-modif` dans `master` (attention : pour une fusion, il faut être sûr d'être sur la branche `master` avant d'initier le _merge_)
    - cela crée-t-il un nouveau _commit_ ou non et pourquoi ?
    - Maintenant, on _push_ la branche `master`
    - On peut finalement supprimer la branche `sa-modif`

- À ce stade, Jean-Michel a son dépôt local qui est « un _commit_ en retard » par rapport au dépôt distant : il ne « voit » pas les modifications faites par Sylvie-Arnaude

- Mais pour l'instant, Sylvie-Arnaude continue à travailler localement :

  - elle liste les branches courantes (normalement une seule) en utilisant le paramètre `-vv` (_very verbose_) de la commande `git branch`
  - elle crée une nouvelle branche `sa-fonctionnalite` basée sur `master` et _switch_ dessus
  - elle modifie le fichier `sa-fichier1.md`
  - elle indexe la modification et _commit_
  - elle liste de nouveau les branches en _very verbose_ et note que la nouvelle branche ne possède pas d'équivalent sur le _remote_
  - elle _push_ en créant la nouvelle branche sur le _remote_
  - elle liste encore les branches et note le pointeur `origin/sa-fonctionnalite` qui a été créé ; il y a donc trois branches qui permettent de gérer `sa-fonctionnalite` :
    - la branche locale `sa-fonctionnalite`
    - la branche _ramote_ `sa-fonctionnalite`
    - la branche de _tracking_ `origin/sa-fonctionnalite` qui permet à Git de relier les deux autres branches ; on ne peut pas manipuler directement cette branche, mais Git s'en sert pour la sunchronisation ; quand on _push_ depuis la branche `sa-fonctionnalite`, les trois branches pointent sur le même _commit_

- À ce stade, Jean-Michel a deux _commits_ de retard en local (mais un seul par rapport à _master_) et ne connaît pas non plus la branche `sa-fonctionnalite`

- Jean-Michel commence maintenant à travailler :
  - il liste les branches en _very verbose_
  - il crée une branche `jm-fonctionnalite` et s'y déplace
  - il crée un nouveau fichier `jm-fichier1.md`
  - il l'indexe et _commit_
  - il liste les branches et note et note que la nouvelle branche n'a pas de branche de _tracking_ associée, et donc pas de _remote branch_
  - il _push_ en créant la branche de _tracking_
  - il liste de nouveau les branches et note que la _tracking branch_ existe

- Combien y a-t-il de branches (en incluant les branches de _tracking_) sur le dépôt local de Jean-Michel ?

- Combien y a-t-il de branches sur le *remote* ?

- Les branches `jm-fonctionnalite`, `origin/jm-fonctionnalite` et la branche _remote_ `jm-fonctionnalite` pointent toutes vers le même *commit* : vrai ou faux ?

- Le clone de Sylvie-Arnaude connaît-il la branche `jm-fonctionnalite` ?

- Jean-Michel fait un _pull_ pour récupérer le travail de Sylvie-Arnaude

- Sylvie-Arnaude fait de même pour récupérer le travail de Jean-Michel

- Souvenez-vous que la commande _pull_ fait deux choses :

  - récupérer (_fetch_) les nouveaux _commits_ et les nouvelles branches depuis le _remote_
  - fusionner (_merge_) ces modifications localement : cela peut potentiellement provoquer des conflits, comme nous l'avons vu précédemment ; ceux-ci seront résolus manuellement de la même manière

- Simulez du travail sur les deux clones dans le but de provoquer un conflit au moment du _pull_ chez Sylvie-Arnaude

  - Résolvez les conflits localement
  - Utilisez une _Pull Request_ pour proposer la résolution en _remote_
