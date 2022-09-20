## TP 01 - Manipulation de variables, entrées et sorties

### Exercice 1

Disons qu’il est 12 h 34 min 56 s (utilisez des variables). Écrire un programme affiche le nombre de secondes écoulées depuis minuit. La sortie (l'affichage à l'écran) ressemblera à :

```
Il est 12 h 34 min 56 s.
Il s'est écoulé xxxxx secondes depuis minuit.
```

`xxxxx` étant bien entendu calculé dans le programme et remplacé dans la sortie.

### Exercice 2

Même chose mais l'heure exacte courante est demandée à l'utilisateur :

```
Entrez les heures :
12
Entrez les minutes :
34
Entrez les secondes :
56

Il est 12 h 34 min 56 s.
Il s'est écoulé xxxxx secondes depuis minuit.
```

### Exercice 3

Même chose que 2 mais la sortie précise cette fois le nombre de secondes *avant* minuit :

```
Entrez les heures :
12
Entrez les minutes :
34
Entrez les secondes :
56

Il est 12 h 34 min 56 s.
Il y a encore xxxxx secondes avant minuit.
```

### Exercice 4

Maintenant il est 15 h 27 min 12 s (ça vous a pris super longtemps). Calculez le pourcentage de temps écoulé depuis le début de l'exercice par rapport aux 24 heures d'une journée. Considérez l'utilisation de nombres flottants pour afficher ce pourcentage avec décimales. N’hésitez pas à utiliser des variables intermédiaires (même si vous n'avez pas à les afficher) pour vous faciliter la tâche et rendre le code plus lisible.

### Exercice 5

Le but est de programmer un tout petit jeu, une sorte de « Devinez le nombre ». Une fois terminé, ça ressemble à ça :

```
Je pense à un nombre entre 1 et 100 inclus. Devinez lequel.
Entrez un nombre : 36
Vous proposez : 36
Le nombre auquel je pensais était : 47
Vous étiez à 11 de la bonne réponse.
```

Vous aurez besoin de générer un nombre aléatoire entre 1 et 100. Renseignez-vous sur le type objet `Random` de Java du package `java.util`. Vous verrez qu'il s'utilise un peu comme un objet `Scanner`.

Nous écrirons des versions améliorées de ce jeu au fur et à mesure de notre apprentissage.
