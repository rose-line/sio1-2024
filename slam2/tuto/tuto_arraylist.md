# Tuto sur l'utilisation de tableaux dynamiques (_ArrayList_)

## Introduction

Un **tableau dynamique** est une collection de données homogènes (de même type) dont le nombre peut changer au cours du déroulement du programme. Par exemple, les joueurs connectés à une session d'un jeu en ligne pourraient être stockés dans un tableau dynamique : elle contient un certain nombre de joueurs à un moment donné, et des joueurs « arrivent » et « repartent » constamment. Cela revient à ajouter/retirer des éléments (des objets _Joueur_) du tableau.

## La classe _ArrayList_

En Java, on utilise la classe `ArrayList` pour créer des tableaux dynamiques. Cette classe est définie dans le package `java.util`, qu'il faudra donc importer.

## Déclaration et initialisation

Pour déclarer et initialiser un tableau dynamique, on utilise la syntaxe suivante :

```java
ArrayList<LeTypeDesElements> lesElements = new ArrayList<>();
```

`lesElements` est le nom du tableau dynamique. `LeTypeDesElements` est le type des éléments du tableau dynamique. Par exemple, si on veut stocker des objets de type `Joueur`, on écrira :

```java
ArrayList<Joueur> lesJoueurs = new ArrayList<>();
```

C'est similaire à ce que vous connaissez déjà pour la déclaration et l'initialisation d'objets classiques. Le seul point qui diffère est que le type des éléments du tableau est précisé entre chevrons `<>`.

Un tableau dynamique ainsi déclaré est vide. Nous allons voir comment ajouter des éléments. Mais d'abord, définissons le type `Joueur`, que nous allons utiliser pour illustrer l'utilisation des tableaux dynamiques.

## La classe `Joueur`

Voici une ébauche de classe représentant un joueur :

```java
public class Joueur {
  private String pseudo;
  private String adresseIP;

  public Joueur(String pseudo, String adresseIP) {
    this.pseudo = pseudo;
    this.adresseIP = adresseIP;
  }

  public String getPseudo() {
    return pseudo;
  }
}
```

Cela nous suffira pour illustrer la suite.

## Ajout d'éléments

Pour ajouter un élément à un tableau dynamique, on utilise la méthode `add` :

```java
ArrayList<Joueur> lesJoueurs = new ArrayList<>();
Joueur unJoueur = new Joueur("Agagada", "88.160.178.154");
lesJoueurs.add(unJoueur);
Joueur unAutreJoueur = new Joueur("Bababada", "88.58.127.10");
lesJoueurs.add(unAutreJoueur);
```

L'elément est alors ajouté à la fin du tableau dynamique. On peut ajouter autant d'éléments que l'on veut.

## Accès aux éléments

La méthode `get` permet d'accéder à un élément du tableau dynamique, en précisant son indice :

```java
Joueur joueur = lesJoueurs.get(0);  // premier élément, les tableaux sont indexés à partir de 0
```

## Parcours du tableau dynamique

Pour parcourir un tableau dynamique, on utilise une boucle `for` « améliorée ». La syntaxe est la suivante :

```java
for (LeTypeDesElements element : lesElements) {
  // instructions à répéter pour chaque element
}
```

Par exemple, pour parcourir le tableau dynamique `lesJoueurs` défini ci-dessus et afficher tous les pseudos des joueurs, on écrira :

```java
for (Joueur joueur : lesJoueurs) {
  System.out.println(joueur.getPseudo());
}
```

Cette séquence se lit : « pour chaque `joueur` de type `Joueur` du tableau `lesJoueurs`, affiche le pseudo du `joueur` ».

## Changement d'un élément

La méthode `set` permet de modifier un élément du tableau dynamique, en précisant son indice :

```java
Joueur joueurQuiRemplace = new Joueur("Cacacada", "88.62.1.120");
lesJoueurs.set(0, joueurQuiRemplace);  // remplace le premier élément par joueurQuiRemplace
```

## Suppression d'éléments

La méthode `remove` permet de supprimer un élément du tableau dynamique, en précisant son indice :

```java
lesJoueurs.remove(0);  // supprime le premier élément
```

## Remise à zéro du tableau

La méthode `clear` permet de supprimer tous les éléments du tableau dynamique :

```java
lesJoueurs.clear();  // après cette instruction, le tableau est vide
```

## Savoir si un tableau est vide

La méthode `isEmpty` permet de savoir si un tableau dynamique est vide :

```java
if (lesJoueurs.isEmpty()) {
  // le tableau est vide
}
```

## Taille du tableau dynamique

La méthode `size` permet de connaître la taille du tableau dynamique :

```java
int taille = lesJoueurs.size();
```

## Test de présence d'un élément

La méthode `contains` permet de savoir si un élément donné est présent dans le tableau :

```java
if (lesJoueurs.contains(unCertainJoueur)) {
  // unCertainJoueur est présent dans le tableau
}
```

## Cas particulier : types de base

Si on a besoin de stocker des valeurs de types de base (entiers, flottants, caractères, booléens), on doit utiliser les classes correspondantes (`Integer`, `Double`, `Character`, `Boolean`) :

```java
ArrayList<Integer> lesEntiers = new ArrayList<>();
```

C'est nécessaire car les types de base ne sont pas des objets. On ne peut donc pas les stocker dans un tableau dynamique. Donc `ArrayList<int> lesEntiers` n'est pas possible.

## Programme complet

Voici un programme complet qui illustre l'utilisation des tableaux dynamiques. Vous pouvez l'inclure dans un projet et expérimenter par vous-même en modifiant le code ou en adaptant à un autre type d'éléments que `Joueur`.

```java
import java.util.ArrayList;

public class TestTableauDynamique {
  public static void main(String[] args) {
    ArrayList<Joueur> lesJoueurs = new ArrayList<>();
    Joueur unJoueur = new Joueur("Agagada", "88.160.178.154");
    lesJoueurs.add(unJoueur);
    Joueur unAutreJoueur = new Joueur("Bababada", "88.58.127.10");
    lesJoueurs.add(unAutreJoueur);

    // On remplace Babadada par Cacacada
    Joueur joueurQuiRemplace = new Joueur("Cacacada", "88.62.1.120");
    lesJoueurs.set(0, joueurQuiRemplace);

    // On affiche tous les pseudos
    for (Joueur joueur : lesJoueurs) {
      System.out.println(joueur.getPseudo());
    }

    // On teste si un objet joueur particulier est présent
    if (lesJoueurs.contains(unJoueur)) {
      // ceci ne va pas s'afficher, le joueur Agagada n'est plus dans le tableau
      System.out.println("Le joueur est présent");
    }

    int taille = lesJoueurs.size();
    System.out.println("Taille du tableau : " + taille);  // affiche 2

    // On supprime le premier joueur
    lesJoueurs.remove(0);

    // On supprime tout le monde finalement
    lesJoueurs.clear();

    if (lesJoueurs.isEmpty()) {
      System.out.println("Le tableau est vide");  // va effectivement s'afficher
    }
  }
}
```
