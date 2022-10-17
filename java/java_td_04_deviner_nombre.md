# Jeu « Deviner le nombre »

Nous allons mettre en place et améliorer au fur et à mesure le jeu « Deviner le nombre » introduit lors d'un TP précédent.

## Version 1 - Base (reprise du TP 01)

Le but est de programmer un petit jeu, une sorte de « Devinez le nombre ». Une fois terminé, vous devez avoir exactement la sortie suivante (excepté bien sûr le nombre à deviner et la proposition du joueur, qui vont changer à chaque exécution) :
____________________________________________________________

Je pense à un nombre entre 1 et 100 inclus. Devinez lequel.
Entrez un nombre : 36
Vous proposez : 36
Le nombre auquel je pensais était : 47
Vous étiez à 11 de la bonne réponse.
____________________________________________________________

Le nombre à deviner doit être généré aléatoirement.

----

## Version 2 - Trop petit/grand

Changez la sortie pour indiquer si votre nombre était trop grand ou trop petit. Le programme indiquera par exemple : `Perdu ! Vous avez dépassé de 34` ou bien `Perdu ! Il vous manquait 12`. Si on a gagné, le programme doit afficher : `Quel bol, vous avez trouvé !`

----

## Version 3 - On recommence jusqu'au gain

On ne s'arrête désormais plus après une proposition. Le programme redemande une proposition jusqu'à ce que le joueur gagne. À la fin, on affiche le nombre de tentatives qui ont été nécessaires.
____________________________________________________________

Je pense à un nombre entre 1 et 100 inclus. Devinez lequel.
Entrez un nombre : 36
Trop grand.
Entrez un nombre : 30
Trop grand.
Entrez un nombre : 19
Trop petit.
Entrez un nombre : 23
Gagné !
Il vous a fallu 4 tentatives.
____________________________________________________________

----

## Version 4 - Faire jouer l'ordi

Dans cette version, c'est l'ordinateur qui joue tout seul : il génère un nombre qu'il doit lui-même deviner. Bien sûr, le programme ne doit pas utiliser le fait qu'il connaît en réalité le nombre pour gagner (pas de triche !).
____________________________________________________________

Une partie de moi pense à un nombre entre 1 et 100 inclus. Une autre partie de moi va essayer de trouver ce nombre.
Je tente : 59
Trop grand.
Je tente : 87
Trop grand.
Je tente : 23
Trop petit.
Je tente : 55
Trop grand.
Je tente : 43
Gagné !
Il m'a fallu 5 tentatives.
____________________________________________________________

----

## Version 5 - Plusieurs parties

Simulez plusieurs parties de l'ordinateur et calculez la moyenne de tentatives sur toutes les parties. Testez d'abord sur 3 ou 4 parties pour voir si votre algorithme fonctionne et si la moyenne est correcte :
____________________________________________________________

Une partie de moi pense à un nombre entre 1 et 100 inclus. Une autre partie de moi va essayer de trouver ce nombre.
Je tente : 3
Trop petit.
Je tente : 61
Trop petit.
...
Je tente : 77
Gagné ! Il m'a fallu 126 tentatives.

Une partie de moi pense à un nombre entre 1 et 100 inclus. Une autre partie de moi va essayer de trouver ce nombre.
Je tente : 14
Trop grand.
Je tente : 38
Trop grand.
...
Je tente : 6
Gagné ! Il m'a fallu 32 tentatives.

Une partie de moi pense à un nombre entre 1 et 100 inclus. Une autre partie de moi va essayer de trouver ce nombre.
Je tente : 84
Trop grand.
Je tente : 24
Trop petit.
...
Je tente : 35
Gagné ! Il m'a fallu 67 tentatives.

En moyenne, sur 3 parties, il m'a fallu 52 tentatives.
____________________________________________________________

## Version 6 - Statistiques V2

On cherche à savoir combien de tentatives il faut en moyenne à l'ordinateur pour gagner. Pour se rapprocher fortement de la moyenne mathématique de notre stratégie (qu'on ne sait pas calculer !), on va faire jouer un très grand nombre de parties à l'ordinateur (10000 sera suffisamment significatif). Pour éviter d'avoir une sortie très grande (et lente), on ne va plus afficher tout le détail pour chaque partie, mais seulement une ligne par partie, qui contiendra :

- le numéro de la partie ;
- la liste des nombres tentés, jusqu'au nombre cible
- entre crochets `[]`, le nombre de tentatives pour cette partie.

Voici un extrait exemple de sortie pour 10000 simulations :
____________________________________________________________

1 - 81 97 15 51 31 41 29 35 49 99 80 21 43 14 48 26 17 28 95 59 49 23 86 83 55 69 45 69 13 8 33 81 54 44 7 64 98 27 12 48 12 23 86 88 73 66 30 [47]
2 - 55 90 14 1 97 81 94 1 57 90 44 57 4 38 83 58 81 79 68 17 64 80 85 8 80 1 1 8 67 5 23 42 41 13 [34]
3 - 7 16 63 53 4 49 38 46 8 92 13 94 44 84 14 16 6 74 35 75 46 3 92 76 59 7 30 63 73 74 4 41 45 18 30 69 12 13 18 71 61 [41]
...
9999 - 94 68 45 99 32 26 [6]
10000 - 55 90 14 1 97 81 94 1 57 90 44 57 4 38 83 58 81 79 68 17 64 80 85 8 80 1 1 8 67 5 23 42 41 13 [34]

En moyenne, sur 10000 parties, il m'a fallu 99,47 tentatives.
____________________________________________________________

## Version 7 - Optimisation

Les exemples ci-dessus montrent un programme qui tente un nombre aléatoire à chaque fois, sans prendre en compte les indications-réponses (trop petit/grand) ni les nombres qu'il a déjà tentés. Cela nous donne, en moyenne, environ 100 tentatives pour trouver à chaque partie !

Votre propre simulation se comporte-t-elle mieux ? Essayez d'améliorer au maximum la moyenne du nombre de tentatives.

(on supprimera maintenant tout affichage en dehors de la moyenne, cela accélèrera l'exécution)
