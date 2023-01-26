# Tuto sur une classe simple illustrant l'encapsulation

On va suivre pas à pas l'implémentation d'une classe simple avec encapsulation (accès aux données contrôlées), comme dans le cours. La classe est une modélisation triviale d'un rectangle.

## Une classe _Rectangle_

Il s'agit ici de définir une classe _Rectangle_ représentant une abstraction de ce qu'est un rectangle : une largeur, une
longueur et sa surface.

Repartez d'un projet dédié pour ce tuto (relire la [procédure de création de projet avec Maven](../../java/installation.md#créer-un-projet-java)). Il vous est conseillé, de toute façon, de créer un projet pour chaque programme. Cela vous permet :

1. de faire gérer ce projet par Git
2. d'avoir un dépôt synchronisé sur GitHub dédié à ce projet
3. de référencer ce projet dans votre portfolio et votre portefeuille de compétences, dans la perspective de l'oral (E4)

Créez un fichier `Rectangle.java` au même niveau que le fichier `App.java`. VS Code remplira automatiquement ce fichier avec une classe _Rectangle_ vide. Le nom du package sera différent de celui spécifié ici, en fonction de ce que vous aurez indiqué lors de la création du projet.

```java
package fr.pgah.tuto;

public class Rectangle {

}
```

## Code client

Dans la méthode `main` du fichier `App.java`, nous allons déclarer et instancier un objet de la classe _Rectangle_. Cela se fait
comme pour n'importe quelle autre variable (_int_, _double_...) : la classe _Rectangle_ étant simplement un nouveau type.

```java
public class App {

  public static void main(String[] args) {
    Rectangle rect = new Rectangle();
  }
}
```

Cela appelle le _constructeur par défaut_ automatiquement créé par Java lorsque vous n'implémentez pas de constructeur dans la classe instanciée.

## Classe _Rectangle_ - État

Revenons sur la classe _Rectangle_ et implémentons la partie « état » (« les données qui caractérisent un rectangle »). On nous parle de longueur, largeur et surface. Les deux premières données sont effectivement à retenir, mais la surface peut être _calculée_ à partir des longueur/largeur. Il nous faut deux attributs `longueur` et `largeur` et une méthode pour la surface, par exemple `calculerSurface`. Commençons par les attributs, appelés aussi *variables d'instance* :

```java
public class Rectangle {
  double longueur;
  double largeur;
}
```

Ces variables sont **accessibles depuis toutes les méthodes de la classe**, contrairement à une variable déclarée à l'intérieur d'une méthode (accessible uniquement dans la méthode).

## Constructeur

La prochaine étape est la définition d'un _constructeur_ pour notre classe. Un constructeur doit initialiser l'objet avec des valeurs cohérentes, en s'aidant potentiellement de ses _paramètres_ pour recevoir des données externes. Ici le constructeur va recevoir une longueur et une largeur de la part de l'appelant :

```java
public class Rectangle {
  double longueur;
  double largeur;

  public Rectangle(double longueur, double largeur) {
    this.longueur = longueur;
    this.largeur = largeur;
  }
}
```

## Comportement - Méthode _calculerSurface_

Pour le calcul de la surface, nous implémentons la méthode `calculerSurface`. Cette méthode :

- ne prend rien en paramètre (entre parenthèse) : elle n'a besoin que de la longueur et de la largeur, et elle en dispose déjà par l'intermédiaire des variables d'instance auxquelles elle a déjà accès ;
- renvoie un _double_ (type de retour) : c'est le type de ce qu'elle va renvoyer à l'appelant (la surface calculée) ;
- et fait donc un _return_ de cette surface calculée.

```java
public class Rectangle {
  double longueur;
  double largeur;

  public Rectangle(double longueur, double largeur) {
    this.longueur = longueur;
    this.largeur = largeur;
  }

  public double calculerSurface() {
    return longueur * largeur;
  }
}
```

## Utilisation du constructeur et appel de la méthode de calcul

La méthode `main` de la classe `App` ne compile plus à présent : l'erreur indique que le constructeur sans paramètre de _Rectangle_ n'existe plus. En effet, lorsque l'on implémente un constructeur, Java ne fournit plus automatiquement un constructeur par défaut. De toute façon, on va modifier l'instanciation pour utiliser notre nouveau constructeur. On va aussi tester la méthode `calculerSurface` en l'appelant et en affichant son résultat :

```java
public static void main(String[] args) {
  Rectangle rect = new Rectangle(10.5, 10);
  double surface = rect.calculerSurface();
  System.out.println("Surface = " + surface);
}
```

Exécutez ce programme. La sortie devrait être la suivante :

```
Surface = 105.0
```

## Accès direct en écriture aux attributs

Supposons maintenant que nous souhaitions modifier les valeurs des attributs dans le programme principal, en utilisant la notation pointée pour y accéder directement :

```java
public static void main(String[] args) {
  Rectangle rect = new Rectangle(10.5, 10);
  double surface = rect.calculerSurface();
  System.out.println("Surface = " + surface);
  rect.longueur = 20.5;
  rect.largeur = 20;
  surface = rect.calculerSurface();
  System.out.println("Surface = " + surface);
}
```

Exécutez le programme. La sortie devrait être la suivante :

```
Surface = 105.0
Surface = 410.0
```

Cela fonctionne comme prévu. Cependant, ces accès directs pour modifier les valeurs des attributs « cassent » l'encapsulation de la classe _Rectangle_. Ainsi, rien n'empêche par exemple un code client de mettre une valeur négative dans la longueur :

```
public static void main(String[] args) {
  Rectangle rect = new Rectangle(10.5, 10);
  rect.longueur = -20.5;
  rect.largeur = 20;
  surface = rect.calculerSurface();
  System.out.println("Surface = " + surface);
}
```

La sortie de ce programme est : `Surface = -410.0`. Cela n'a évidmment pas de sens : en permettant au client (`main`) de modifier directement les attributs de la classe, on a pris le risque de rendre notre objet dans un **état instable**, c'est-à-dire avec des données incohérentes et des comportements résultants problématiques.

## Encapsulation

C'est pourquoi nous allons appliquer les principes d'**encapsulation** à notre classe. On va rendre privés les attributs et ne laisser public que les méthodes qui représentent les « services » de la classe. Actuellement, on n'a spécifié aucun modificateur d'accès sur les attributs. Cela les rend « privés au package » (_package-private_), c'est-à-dire que toutes les classes du package `fr.pgah.tuto` y ont accès. Rendons ces attributs complètement privés à la classe gràce au modificateur d'accès `private` :

```java
public class Rectangle {
  private double longueur;
  private double largeur;

  public Rectangle(double longueur, double largeur) {
    this.longueur = longueur;
    this.largeur = largeur;
  }

  public double calculerSurface() {
    return longueur * largeur;
  }
}
```

Le programme ne compile alors plus : le compilateur indique les attributs sont privés, et qu'on ne peut pas les utiliser hors de l'objet : ils ne font pas partie de **l'interface publique** de l'objet. En particulier, on n'a pas le droit d'écrire `rect.largeur` dans la méthode `main`.

## Définition de _getters_ et de _setters_

Pour rendre accessible depuis l'extérieur un attribut, il faut définir des _getters_ (accès en lecture) et/ou des _setters_ (accès en écriture) pour chaque attribut souhaité. Ce sont des méthodes publiques qui permettent un accès **indirect** aux attributs.

On n'écrit des _getters_/_setters_ que lorsqu'on en a réellement besoin dans le code : tant que les clients de la classe n'ont pas d'intérêt à accéder aux attributs privés, il faut éviter de les « tenter ». Ici, on va imaginer que l'on a effectivement besoin de manipuler en lecture et en écriture les longueur et largeur d'un objet _Rectangle_ depuis l'extérieur. On va donc écrire les deux couples _getters_/_setters_.

Au niveau des _setters_, cela va nous permettre de vérifier qu'on ne met pas de valeurs négatives ou nulles dans les attributs _longueur_ et *largeur* : de telles valeurs provoqueront l'affichage d'une erreur et seront ensuite ignorées. Cela s'appelle du « contrôle d'intégrité des données ». On pourrait aussi ici faire du contrôle d'accès par exemple : l'entité qui tente de modifier la donnée a-t-elle les droits pour cela ?

```java
public class Rectangle {
  private double longueur;
  private double largeur;

  public Rectangle(double longueur, double largeur) {
    this.longueur = longueur;
    this.largeur = largeur;
  }

  public double getLongueur() {
    return longueur;
  }

  public void setLongueur(double nouvelleLongueur) {
    if (nouvelleLongueur <= 0) {
      System.out.println("La longueur doit être positive");
      return;
    }
    this.longueur = nouvelleLongueur;
  }

  public double getLargeur() {
    return largeur;
  }

  public void setLargeur(double nouvelleLargeur) {
    if (nouvelleLargeur <= 0) {
      System.out.println("La largeur doit être positive");
      return;
    }
    this.largeur = nouvelleLargeur;
  }

  public double calculerSurface() {
    return longueur * largeur;
  }
}
```

## Utilisation des _getters_/_setters_

Le code client utilisant les deux _setters_ devient alors :

```java
public static void main(String[] args) {
  Rectangle rect = new Rectangle(10.5, 10);
  double surface = rect.calculerSurface();
  System.out.println("Surface = " + surface);
  rect.setLongueur(20.5);
  rect.setLargeur(20);
  surface = rect.calculerSurface();
  System.out.println("Surface = " + surface);
}

SORTIE DU PROGRAMME :

Surface = 105.0
Surface = 410.0
```

Si l'on essaie de nouveau de mettre une valeur négative ou nulle dans un attribut, le code de contrôle d'intégrité du _setter_ va nous en empêcher : un message d'erreur est affiché sur la console et la valeur sera ignorée. Le code client suivant illustre cela et utilise aussi les _getters_ définis pour afficher les caractéristiques du rectangle avant les calculs de surface :

```java
public static void main(String[] args) {
  Rectangle rect = new Rectangle(10.5, 10);
  System.out.println("Longueur = " + rect.getLongueur());
  System.out.println("Largeur = " + rect.getLargeur());
  double surface = rect.calculerSurface();
  System.out.println("Surface = " + surface);
  rect.setLongueur(-20.5);
  rect.setLargeur(20);
  System.out.println("Longueur = " + rect.getLongueur());
  System.out.println("Largeur = " + rect.getLargeur());
  surface = rect.calculerSurface();
  System.out.println("Surface = " + surface);
}

SORTIE DU PROGRAMME :

Longueur = 10.5
Largeur = 10.0
Surface = 105.0
La longueur doit être positive
Longueur = 10.5
Largeur = 20.0
Surface = 210.0
```
