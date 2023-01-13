# TP Mentalisme

## Introduction

Il s'agit d'élaborer, en POO, une simulation de la réalisation d'un tour de magie de type « mentalisme », c'est-à-dire dans lequel le magicien « devine » des informations qui concerne un spectateur.

## Description de la solution

Ce tour met en scène le magicien mentaliste, son assistant, et un spectateur. Voici son déroulement :

1. Le mentaliste demande à un spectateur d'écrire sur un papier son âge et la somme qu'il a en poche (maximum 99 €, arrondi à l'entier près).
2. L'assistant doit ensuite le lire (sans rien dire), puis effectuer secrètement le calcul suivant : multiplier l'âge par 2, lui ajouter 5, multiplier le résultat par 50, ajouter la somme en poche, et soustraire le nombre de jours que contient une année, puis finalement donner le résultat à haute voix.
3. En ajoutant mentalement 115 au chiffre reçu, le magicien trouve tout de suite l'âge et la somme en poche (qui étaient restés secrets). Il lui suffit de séparer en deux le nombre à 4 chiffre ainsi obtenu.

Vous devez modéliser les classes _Magicien_, _Assistant_, _Spectateur_ et _Papier_, en définissant leurs attributs (état) et leurs méthodes (comportement). Vous préserverez l'encapsulation en mettant tous les attributs en _private_ et en ne défissant _getters_ et _setters_ que cela s'avère nécessaire. Vous définirez des constructeurs pour ces classes en fonction des besoins que vous jugerez nécessaires.

Pour la classe _Spectateur_ en particulier, on fournira deux constructeurs différents :

- un constructeur non paramétré qui demandera explicitement, sur le terminal, l'âge du spectateur ainsi que la somme d'argent qu'il a en poche ;
- un constructeur paramétré (âge et somme en poche reçus en paramètres).

Dans les deux cas, le constructeur imposera une somme d'argent maximum de 99 €. Vous testerez les deux constructeurs dans votre code client (deux exemples d'exécution différents).

## Exemple d'exécution

```
[Spectateur] J'entre mon âge : 53
[Spectateur] J'entre la somme d'argent que j'ai en poche (max 99) : 112
[Spectateur] J'entre la somme d'argent que j'ai en poche : 28
[Assistant] Bonjour, Spectateur !
[Assistant] Veuillez écrire sur ce bout de papier votre âge et la somme d'argent que vous avez en poche.
[Spectateur] J'écris les informations et je donne le papier à l'assistant.
[Assistant] Bien ! Je prends le papier et je le lis silencieusement...
[Assistant] J'annonce : 5213 !
[Magicien] Mmm... Vous avez 53 ans et vous avez 28 euros en poche !
```

## Conseils

- Réfléchissez bien aux attributs : _qui a quoi, comme données (état) ?_
- Et aux méthodes : _qui fait quoi ?_ Il faudra demander l'âge et la somme au spectateur, écrire sur un papier, montrer le papier, lire le papier, faire le calcul, etc. Toutes ces actions sont de potentiels indices pour définir des méthodes de certaines classes.
- Mais même pour cette petite simulation, il y a de multiples variantes d'implémentation possibles. Il n'y a pas de solution unique.
- C'est votre code client qui va vous indiquer si votre modélisation est plutôt bonne et cohérente : si le code client se lit un peu comme le déroulement du tour et s'adresse à chaque fois aux objets concernés, ça veut dire que que l'implémentation de vos classes est probablement cohérente.
- Pour cette raison, il vous est conseillé de commencer par le code client, avant d'implémenter les classes : qu'aimeriez vous écrire pour la première phase du tour dans votre code client ? Puis commencer à implémenter la classe correspondante pour répondre à ce besoin.
- Travaillez étape par étape, testez le plus rapidement possible et au fur et à mesure.
