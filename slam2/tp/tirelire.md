# TP Tirelire

## Introduction

Le but de cet exercice est de simuler une tirelire dans laquelle on stocke et retire de l'argent et que l'on souhaite utiliser pour payer un certain budget (vacances...).

## Description de la solution

Créez un nouveau projet Java (_tirelire_) et faire en sorte que la méthode _main_ de la classe principale soit comme il suit :

```java

```

Le code fourni crée une tirelire et lui fait subir diverses manipulations (la vider, la secouer, en afficher le contenu, etc.). Ce programme demande aussi à l'utilisateur quel budget il aimerait consacrer à ses vacances. Si la tirelire contient suffisamment d'argent, il indique combien d'argent il resterait dans la tirelire après les vacances. Dans la cas contraire, il indique quel montant manque pour partir en vacances avec le budget souhaité.

Le code fourni n'est pas compilable car la classe _Tirelire_ n'est pas fournie. Il vous est demandé de l'implémenter.

Une tirelire est caractérisée par le montant qu'elle contient. Les traitements qui lui sont spécifiques sont :

- un constructeur sans paramètre : initialise le montant à zéro

- un constructeur avec un paramètre `montant` : initialise le montant à une valeur initiale fournie

- une méthode `getMontant` : renvoie le montant de la tirelire

- une méthode `vider` : (ré)intialise le montant de la tirelire à zéro

- une méthode `getCaractéristiques` : renvoie les caractéristiques données de la tirelire sous le format suivant :

  - `"Vous êtes sans le sou..."`, si la tirelire est vide
  - `"Vous avez <montant> euros dans la tirelire."`, sinon

- une méthode `secouer` :

  - affiche le message `"gling gling !"` sur la sortie si la tirelire n'est pas vide
  - ne fait rien sinon

- une méthode `ajouter` : met dans la tirelire un montant passé en paramètre (type _double_, on ne considérera pas les problèmes que ce type pose avec les valeurs monétaires) ; seuls les montants positifs seront acceptés (dans le cas contraire on ne fait rien).

- une méthode `sortir` : retire de la tirelire un montant passé en paramètre ; si le montant est négatif, il sera ignoré ; si le montant est plus grand que le montant disponible, la tirelire est alors vidée. La méthode ne renvoie rien.

- une méthode `soldeSiOnSort` qui renvoie la différence entre le montant de la tirelire et la somme indiquée en paramètre (un _double_). La méthode peut donc renvoyer une valeur potentiellement négative si la somme indiquée est supérieure au montant de la tirelire. Si la somme en paramètre est elle-même négative, la méthode doit renvoyer le montant de la tirelire.

Toutes ces méthodes feront partie de l’interface publique de la classe.

## Exemple d'exécution

Les deux exemples suivants sont tirés de l'exécution de la méthode `main` définie précédemment. La sortie est différente parce que l'utilisateur ne rentre pas le même budget-vacances.

- Exemple dans lequel l'utilisateur entre un budget (446 €) dépassant le total de la tirelire :

```
Vous êtes sans le sou...
Vous êtes sans le sou...
Gling gling !
Vous avez 500,00 euros dans la tirelire.
Vous avez 445,00 euros dans la tirelire.
Indiquez le budget de vos vacances : 446
Il vous manque 1.0 euros pour partir en vacances...
```

- Exemple dans lequel l'utilisateur indique un budget moindre :

```
Vous êtes sans le sou...
Vous êtes sans le sou...
Gling gling !
Vous avez 500,00 euros dans la tirelire.
Vous avez 445,00 euros dans la tirelire.
Indiquez le budget de vos vacances : 440
Vous êtes assez riche pour partir en vacances !
Il vous restera 5.0 euros à la rentrée.
```
