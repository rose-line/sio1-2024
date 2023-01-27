# TP Supermarché

## Introduction

Il s'agit d'afficher le total des achats enregistrés par les caisses d'un supermarché. Le programme `AppSupermache.java` contient une méthode `main` documentant la façon dont on souhaite utiliser le programme. Actuellement, le programme ne compile pas : les classes utilisées par cette méthode ne sont pas implémentées.

## Programme initial

Le programme principal donné ici a pour but de faire afficher le montant total de chaque caisse au bout d'une journée donnée. Commencez par l'étudier. **Vous ne devez pas le modifier pour quelque raison que ce soit**. C'est votre solution qui doit s'adapter à ce programme principal.

```java
package fr.pgah.tp;

public class AppSupermache {
  public static void main(String[] args) {

    // Tous les articles vendus dans le supermarché
    // Constructeur :
    // Le premier paramètre est le nom de l'article
    // Le second est le prix de l'article
    // Le troisième indique si l'article est en promotion
    Article choufleur = new Article("Chou-fleur extra", 3.50, false);
    Article roman = new Article("Les malheurs de Sophie", 8.50, true);
    Article camembert = new Article("Cremeux 100%MG", 3.80, false);
    Article livre = new Article("Java pour les Nuls", 28.50, false);
    Article boisson = new Article("Petit-lait", 2.50, true);
    Article petitspois = new Article("Pois surgeles", 4.35, false);
    Article poisson = new Article("Sardines", 6.50, false);
    Article biscuits = new Article("Cookies de grand-mere", 3.20, false);
    Article poires = new Article("Poires Williams", 4.80, false);
    Article cafe = new Article("100% Arabica", 6.90, true);
    Article pain = new Article("Pain d'epautre", 6.90, false);

    // Les caisses du supermarché
    // Constructeur :
    // Le premier paramètre est le numéro de caisse
    // Le second est le montant initial de la caisse

    Caisse caisse1 = new Caisse(1, 0.0);
    Caisse caisse2 = new Caisse(2, 0.0);

    // Les clients font leurs achats
    // La méthode "remplir" prend une quantité en second paramètre

    Caddie caddie1 = new Caddie();

    caddie1.remplir(choufleur, 2);
    caddie1.remplir(livre, 1);
    caddie1.remplir(biscuits, 4);
    caddie1.remplir(boisson, 6);
    caddie1.remplir(poisson, 2);

    Caddie caddie2 = new Caddie();

    caddie2.remplir(roman, 1);
    caddie2.remplir(camembert, 1);
    caddie2.remplir(petitspois, 2);
    caddie2.remplir(poires, 2);

    Caddie caddie3 = new Caddie();

    caddie3.remplir(cafe, 2);
    caddie3.remplir(pain, 1);
    caddie3.remplir(camembert, 2);

    // Les clients passent aux caisses

    caisse1.scanner(caddie1);
    caisse1.scanner(caddie2);
    caisse2.scanner(caddie3);

    // Fin de journée, on affiche les totaux de chaque caisse

    caisse1.totalCaisse();
    caisse2.totalCaisse();
  }
}
```

## Description de la solution

Il vous est demandé de compléter le programme en implémentant les classes manquantes. Voici les entités nécessaires pour modéliser le fonctionnement du supermarché :

- les articles vendus (classe _Article_) : caractérisés par leur nom (une chaîne de caractères), leur prix unitaire (un _double_) et une information indiquant si l'article est en solde ou pas (un booléen) ;

- les caddies (classe _Caddie_) : caractérisés par l’ensemble des achats qu'ils contiennent ;

- les caisses (classe _Caisse_) : chargées de scanner et enregistrer le contenu des caddies. Une caisse est caractérisée par un numéro de caisse (un entier) et le montant total des achats qu'elle a scannés dans la journée (un _double_). La méthode `scanner` de cette classe va afficher le « ticket de caisse » : date, informations du caddie, montant total.

C'est l'ensemble minimal de classes qu'il faudra implémenter pour faire fonctionner le programme donné. Il vous est cependant suggéré d'implémenter une ou plusieurs autres classes si cela vous semble approprié.

## Exemple d'exécution

La sortie suivante est tirée de l'exécution de la méthode `main` définie précédemment, lorsque toutes les classes annexes sont implémentées correctement. Votre sortie devra être identique.

```
=========================================
27/01/23
Caisse numéro 1

Chou-fleur extra : 3.5 x 2 = 7.0 euros
Java pour les Nuls : 28.5 x 1 = 28.5 euros
Cookies de grand-mere : 3.2 x 4 = 12.8 euros
Petit-lait : 2.5 x 6 = 15.0 euros (remise 50 %) => 7.5 euros
Sardines : 6.5 x 2 = 13.0 euros

Montant à payer : 68.8 euros
=========================================

=========================================
27/01/23
Caisse numéro 1

Les malheurs de Sophie : 8.5 x 1 = 8.5 euros (remise 50 %) => 4.25 euros
Cremeux 100%MG : 3.8 x 1 = 3.8 euros
Pois surgeles : 4.35 x 2 = 8.7 euros
Poires Williams : 4.8 x 2 = 9.6 euros

Montant à payer : 26.35 euros
=========================================

=========================================
27/01/23
Caisse numéro 2

100% Arabica : 6.9 x 2 = 13.8 euros (remise 50 %) => 6.9 euros
Pain d'epautre : 6.9 x 1 = 6.9 euros
Cremeux 100%MG : 3.8 x 2 = 7.6 euros

Montant à payer : 21.4 euros
=========================================

La caisse numéro 1 a encaissé 95,15 euros aujourd'hui
La caisse numéro 2 a encaissé 21,40 euros aujourd'hui
```

## Quelques précisions

- C'est la méthode `scanner` de la classe `Caisse` qui provoque l'affichage du « ticket de caisse » du caddie scanné.

- On pourra utiliser un _tableau dynamique_ (`ArrayList`) pour stocker le contenu d'un caddie (voir le [tuto d'utilisation d'un tableau dynamique](../tuto/tuto_arraylist.md)) ; une bonne question à se poser est celle du type des objets stockés dans ce tableau.

- Notez que l'affichage de la ligne pour un article est différent, selon qu'il est en promotion ou non.

- Le montant total d'une caisse pourra être mis à jour à chaque passage de caddie (dans `scanner`), pour ensuite être simplement affiché au moment de l'appel `totalCaisse()`.

- Pour obtenir la date du jour (affichage sur le ticket), vous pouvez utiliser le code suivant (attention de ne pas importer depuis le package `java.sql` lors de la résolution automatique avec VS Code) :

```java
Date dateDuJour = new Date();
SimpleDateFormat formatDate = new SimpleDateFormat("dd/MM/yy");
String dateFormatée = formatDate.format(dateDuJour);   // exemple : 18/02/2027
```
