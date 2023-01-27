# TP Banque

## Introduction

Le programme `AppBanqueInitial.java` (dont le code est fourni) contient un programme bancaire qui est modularisé sous forme de méthodes auxiliaires. Votre tâche est de le transformer en programme orienté objets.

## Étapes de réflexion

1. Étudiez le fonctionnement du programme. La banque a deux clients. Chaque client a un compte courant et un compte épargne avec des soldes différents. On effectue des opérations (crédit et débit) sur certains comptes de chaque client. Le débit sur un compte épargne entraîne des frais de débit immédiats. Les taux d'intérêt permettent de calculer les intérêts qu'engendrent chaque compte en fin d'année. Le taux d'intérêt d'un compte épargne est plus élevé que celui d'un compte courant. Les données de chaque client (nom, ville et soldes) sont affichées avant et après le bouclement des comptes en fin d'année.

2. Réfléchissez aux objets que vous aimeriez utiliser dans votre programme et ajoutez les classes correspondantes. Il peut s'agir d'objets de toute nature (client, maison, billet, compte, relation bancaire, etc.). N'oubliez pas que la modularisation n'est pas une science exacte. Chaque programmeur décide des classes qu'il trouve utiles et qui lui semblent correspondre au meilleur modèle de la réalité. C'est souvent l'étape la plus difficile d'un projet de programmation.

3. Transférez le code concernant les objets dans les classes. Utilisez le modificateur d'accès `private` pour encapsuler les variables et les méthodes d'instance qui ne seront pas utilisées à l'extérieur de la classe. Chaque méthode (auxiliaire -- private, ou d'instance -- public) doit être courte et sans trop d'instructions détaillées. Les identificateurs (noms des variables et des méthodes) doivent être bien choisis.

## Programme initial

Voici le programme initial, fonctionnel mais pas du tout orienté objets. Votre programme OO devra avoir le même comportement. Commencez par recopier ce programme dans votre solution et exécutez-le. Vérifiez que vous obtenez la sortie indiquée dans la section suivante.

```java
package fr.pgah.tp;

public class AppBanqueInitial {
  public static void main(String[] args) {
    double tauxCompteCourant = 0.01;
    double tauxCompteEpargne = 0.05;
    double fraisDeDébitEpargne = 15;

    String nomClient1 = "Totoro";
    String villeClient1 = "Maubeuge";
    double soldeCourantClient1 = 1000;
    double soldeEpargneClient1 = 2000;

    String nomClient2 = "Shoto";
    String villeClient2 = "Cambrai";
    double soldeCourantClient2 = 3000;
    double soldeEpargneClient2 = 4000;

    System.out
        .println(infosClient(nomClient1, villeClient1, soldeCourantClient1, soldeEpargneClient1));
    System.out
        .println(infosClient(nomClient2, villeClient2, soldeCourantClient2, soldeEpargneClient2));
    System.out.println("** Quelques crédits et débits sur les comptes...**\n");

    soldeCourantClient1 = créditer(soldeCourantClient1, 100);
    soldeCourantClient1 = débiterCourant(soldeCourantClient1, 2000);
    soldeCourantClient1 = créditer(soldeCourantClient1, 900);
    soldeCourantClient1 = débiterCourant(soldeCourantClient1, 2000);
    soldeEpargneClient1 = créditer(soldeEpargneClient1, 1000);

    soldeCourantClient2 = débiterCourant(soldeCourantClient2, 1000);
    soldeEpargneClient2 = débiterEpargne(soldeEpargneClient2, 100, fraisDeDébitEpargne);

    System.out
        .println(infosClient(nomClient1, villeClient1, soldeCourantClient1, soldeEpargneClient1));
    System.out
        .println(infosClient(nomClient2, villeClient2, soldeCourantClient2, soldeEpargneClient2));

    System.out.println("** Ajout des intérêts de fin d'année... **\n");

    soldeCourantClient1 = bouclerCompte(soldeCourantClient1, tauxCompteCourant);
    soldeCourantClient2 = bouclerCompte(soldeCourantClient2, tauxCompteCourant);
    soldeEpargneClient1 = bouclerCompte(soldeEpargneClient1, tauxCompteEpargne);
    soldeEpargneClient2 = bouclerCompte(soldeEpargneClient2, tauxCompteEpargne);

    System.out
        .println(infosClient(nomClient1, villeClient1, soldeCourantClient1, soldeEpargneClient1));
    System.out
        .println(infosClient(nomClient2, villeClient2, soldeCourantClient2, soldeEpargneClient2));
  }

  private static double créditer(double soldeActuel, double montant) {
    double nouveauSolde = soldeActuel + montant;
    return nouveauSolde;
  }

  private static double débiterCourant(double soldeActuel, double montant) {
    if (soldeActuel >= montant) {
      double nouveauSolde = soldeActuel - montant;
      return nouveauSolde;
    }
    // Si le compte n'est pas suffisamment provisionné, le débit n'est pas effectué
    return soldeActuel;
  }

  private static double débiterEpargne(double soldeActuel, double montant, double frais) {
    if (soldeActuel >= montant + frais) {
      double nouveauSolde = soldeActuel - (montant + frais);
      return nouveauSolde;
    }
    // Si le compte n'est pas suffisamment provisionné, le débit n'est pas effectué
    return soldeActuel;
  }

  private static String infosClient(String nom, String ville, double soldeCourant,
      double soldeEpargne) {
    String infos = "Client " + nom + " de " + ville + "\n";
    infos += "    Compte courant : " + soldeCourant + " euros\n";
    infos += "    Compte épargne : " + soldeEpargne + " euros\n";
    return infos;
  }

  private static double bouclerCompte(double solde, double taux) {
    double intérêts = taux * solde;
    double nouveauSolde = solde + intérêts;
    return nouveauSolde;
  }
}
```

## Exemple d'exécution

Voici la sortie du programme initial. Votre version orientée objets devra produire exactement la même sortie.

```
Client Totoro de Maubeuge
    Compte courant : 1000.0 euros
    Compte épargne : 2000.0 euros

Client Shoto de Cambrai
    Compte courant : 3000.0 euros
    Compte épargne : 4000.0 euros

** Quelques crédits et débits sur les comptes...**

Client Totoro de Maubeuge
    Compte courant : 0.0 euros
    Compte épargne : 3000.0 euros

Client Shoto de Cambrai
    Compte courant : 2000.0 euros
    Compte épargne : 3885.0 euros

** Ajout des intérêts de fin d'année... **

Client Totoro de Maubeuge
    Compte courant : 0.0 euros
    Compte épargne : 3150.0 euros

Client Shoto de Cambrai
    Compte courant : 2020.0 euros
    Compte épargne : 4079.25 euros
```

## Évolution

On ajoute le besoin suivant :

- L'affichage des infos client doit indiquer « **Client** Machin de ... » pour le client M. Machin et « **Cliente** Machine de ... » pour la cliente Mme Machine.

Apportez les modifications nécessaires à votre version pour implémenter de nouveau besoin. Exemple de sortie souhaité pour l'affichage des infos d'un client puis d'une cliente :

```
Client Shoto de Cambrai
    Compte courant : 1000.0 euros
    Compte épargne : 2000.0 euros

Cliente Kioka de Lille
    Compte courant : 3000.0 euros
    Compte épargne : 4000.0 euros
```

Regarder comment vous auriez implémenté ce besoin dans le programme initial. Ce serait la même idée, mais cela aurait encore ajouté des informations et des traitements dans la classe principale, déjà bien chargée. La version modularisée en plusieurs classes permet de mieux isoler ce changement et de le rendre plus facile à implémenter. C'est l'un des grands avantages de la POO.
