# Guerre Marine

## Description du projet

Le but est d'implémenter une version du jeu de « Bataille Navale ». Chacun des joueurs choisit l'emplacement de ses navires sur une grille puis tente de couler les navires ennemis en choisissant en tour à tour les coordonnées sur lesquelles frapper.

## Description de la solution demandée

Le programme doit se comporter de la façon suivante :

1. Afficher le message « Bienvenue dans Guerre Marine ! »

2. Demander à chacun des joueurs d'entrer les coordonnées de cinq navires de taille 1 sur une grille de taille 5x5. Il faut donc cinq _prompts_ séparés. On s'attend à ce que le joueur entre deux nombres entiers séparés par un espace. Le premier nombre représente le numéro de ligne et le second le numéro de colonne, par exemple `0 4`.

- Si le joueur entre une séquence invalide, afficher `Coordonnées invalides. Veuillez réessayer.`
- Si le joueur entre des coordonnées déjà entrées, afficher `Vous avez déjà un navire à cet endroit. Choisissez des coordonnées différentes.`
- À la fin de chaque saisie, une grille montrant l'emplacement des navires sera affichée sur la console (voir exemple ci-dessous).
- 100 lignes vides doivent suivre l'affichage de la grille finale d'un joueur afin que le joueur suivant, qui joue sur le même écran, ne voit pas la grille adverse lorsque c'est son tour.

3. Il faut créer et maintenir deux grilles d'état, une pour chaque joueur. Une _grille d'état_ a pour taille 5x5 et conserve l'état du champ de bataille : où sont les navires du joueur ? À quel endroit l'ennemi a-t-il déjà tiré ? Quels sont les navires touchés ? La grille d'état du joueur doit être affichée à la fin de la saisie de ses cinq coordonnées. Pour l'affichage, les conventions suivantes seront utilisées :

- un caractère `-` représente un espace vide ;
- un caractère `@` représente un navire non touché ;
- un caractère `X` représente un navire touché ;
- un caractère `O` représente un coup dans l'eau ;
- au début de la partie effective (après saisie des coordonnées initiales), chaque navire ayant une taille 1, cinq des vingt-cinq espaces d'une grille commenceront donc avec un `@`, le reste étant `-`.

4. Une fois les deux grilles ainsi initialisées, le jeu peut commencer. Chaque joueur lance tour à tour un projectile sur la grille adverse en indiquant les coordonnées d'attaque, sous la même forme que précédemment. Lors de la saisie des coordonnées d'attaque :

- si les coordonnées sont invalides, afficher `Coordonnées invalides. Veuillez réessayer.` ;
- si le joueur a déjà ciblé l'espace précédemment, afficher `Vous avez déjà ciblé cet endroit. Choisissez des coordonnées différentes.` ;
- s'il n'y a pas de navire à l'espace ciblé, afficher `JOUEUR [1/2] : COUP DANS L'EAU !` ;
- s'il y a un navire à l'espace ciblé, afficher `JOUEUR [1/2] A COULÉ UN NAVIRE DU JOUEUR [2/1] !`

5. Après chaque tentative (succès ou non), la grille adverse doit être mise à jour et affichée pour permettre au joueur de suivre la progression de l'attaque. Bien sûr, seuls les espaces sur lesquelles il a déjà tiré doivent révéler des informations. Donc, de son point de vue :

- un caractère `-` représente un espace encore inattaqué ;
- un caractère `X` représente un navire touché ;
- un caractère `O` représente un coup dans l'eau.

6. Le cycle de jeu tour à tour se termine dès qu'un joueur a gagné, c'est-à-dire qu'il a coulé les cinq navires adverses.

- Le programme affiche alors le message `JOUEUR [1/2] A GAGNÉ ! [X] DE VOS NAVIRES SONT ENCORE À FLÔT.`
- Les deux grilles d'état finales doivent ensuite être affichées.

## Contraintes

- Vous concevrez une solution en vous appuyant sur le paradigme de la programmation orientée objets.
- Vous éviterez les méthodes trop longues en modularisant leurs traitements.
- La seule importation autorisée pour la « version de base » est `java.util.Scanner`.
- Vous instancierez un seul objet de type `Scanner` pour tout le programme.
- Le choix des diverses structures de données, notamment pour maintenir les grilles d'état, est laissé libre. Vous veillerez cependant à ce que les détails d'implémentation soient inconnus des clients en utilisant l'encapsulation.

## Exemple de sortie

Respectez le format suivant à la lettre.

```
Bienvenue dans Guerre Marine !

JOUEUR 1, entrez les coordonnées de vos navires, sous la forme "L C"
(L représente la ligne entre 0 et 4 et C la colonne entre 0 et 4).
Entrez les coordonnées du navire 1 : 0 1
Entrez les coordonnées du navire 2 : 1 3
Entrez les coordonnées du navire 3 : 2 1
Entrez les coordonnées du navire 4 : 1 3
Vous avez déjà un navire à cet endroit. Veuillez réessayer.
Entrez les coordonnées du navire 4 : 3 4
Entrez les coordonnées du navire 5 : 3 0

  0 1 2 3 4
0 - @ - - -
1 - - - @ -
2 - @ - - -
3 @ - - - @
4 - - - - -

...
(100 lignes vides)
...

JOUEUR 2, entrez les coordonnées de vos navires, sous la forme "L C"
(L représente la ligne entre 0 et 4 et C la colonne entre 0 et 4).
Entrez les coordonnées du navire 1 : 0 1
Entrez les coordonnées du navire 2 : 0 4
Entrez les coordonnées du navire 3 : 2 0
Entrez les coordonnées du navire 4 : 5 1
Coordonnées invalides. Veuillez réessayer.
Entrez les coordonnées du navire 4 : 4 4
Entrez les coordonnées du navire 5 : 3 1

  0 1 2 3 4
0 - @ - - @
1 - - - - -
2 @ - - - -
3 - @ - - -
4 - - - - @

...
(100 lignes vides)
...

JOUEUR 1, entrez les coordonnées de votre tir :
5 12
Coordonnées invalides. Veuillez réessayer.
JOUEUR 1, entrez les coordonnées de votre tir :
3 2

JOUEUR 1 : COUP DANS L'EAU !

  0 1 2 3 4
0 - - - - -
1 - - - - -
2 - - - - -
3 - - O - -
4 - - - - -

JOUEUR 2, entrez les coordonnées de votre tir :
1 0

JOUEUR 2 : COUP DANS L'EAU !

  0 1 2 3 4
0 - - - - -
1 O - - - -
2 - - - - -
3 - - - - -
4 - - - - -

JOUEUR 1, entrez les coordonnées de votre tir :
3 2
Vous avez déjà ciblé cet endroit. Choisissez des coordonnées différentes.
JOUEUR 1, entrez les coordonnées de votre tir :
0 4

JOUEUR 1 A COULÉ UN NAVIRE DU JOUEUR 2 !

  0 1 2 3 4
0 - - - - X
1 - - - - -
2 - - - - -
3 - - O - -
4 - - - - -

JOUEUR 2, entrez les coordonnées de votre tir :
3 3

JOUEUR 2 : COUP DANS L'EAU !

  0 1 2 3 4
0 - - - - -
1 O - - - -
2 - - - - -
3 - - - O -
4 - - - - -

JOUEUR 1, entrez les coordonnées de votre tir :
2 0

JOUEUR 1 A COULÉ UN NAVIRE DU JOUEUR 2 !

  0 1 2 3 4
0 - - - - X
1 - - - - -
2 X - - - -
3 - - O - -
4 - - - - -

JOUEUR 2, entrez les coordonnées de votre tir :
3 4

JOUEUR 2 A COULÉ UN NAVIRE DU JOUEUR 1 !

  0 1 2 3 4
0 - - - - -
1 O - - - -
2 - - - - -
3 - - - O X
4 - - - - -

...
(coupe jusqu'au dernier tour)
...

JOUEUR 1, entrez les coordonnées de votre tir :
3 1

JOUEUR 1 A COULÉ UN NAVIRE DU JOUEUR 2 !

  0 1 2 3 4
0 - X - - X
1 - - - - -
2 X - - - -
3 - X O - -
4 - - - - X

JOUEUR 1 A GAGNÉ ! 2 DE VOS NAVIRES SONT ENCORE À FLÔT.

Grilles finales :

  0 1 2 3 4
0 - @ O - O
1 O - O @ -
2 O X - O -
3 X O - O X
4 - O - O O

  0 1 2 3 4
0 O X O O X
1 - - - - -
2 X O O O O
3 O X O O -
4 - - - - X
```

## Évolutions

- Taille des grilles paramétrable.

- Variante avec plusieurs types de navires
  - quatre tailles différentes, et un nombre de navire différent pour chaque type :
    - 1 Porte-avions (taille : 4 cases)
    - 2 Croiseurs (3 cases)
    - 3 Torpilleurs (2 cases)
    - 4 Sous-marin (1 case)
  - le placement peut se faire horizontalement ou verticalement pour chaque navire, en prenant soin que les navires ne se « croisent » pas
  - gérer la différence TOUCHÉ/COULÉ
  - la taille standard pour cette variante est 10x10

- Version « joueur contre ordinateur ».

- Version JavaFX.

- Version LAN, en utilisant des sockets pour la communication entre deux machines.
