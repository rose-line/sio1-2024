# Conception d'une interface graphique et accès à une base de données

## Introduction

Ce TP vous donnera les éléments nécessaires pour :

- concevoir une interface graphique et gérer les interactions utilisateur en utilisant le framework _JavaFX_ ;
- accéder à un SGDBR (Système de Gestion de Bases de Données Relationnelles) MySQL afin de manipuler des données depuis une application Java grâce à JDBC (_Java Database Connector_)

## Prérequis

- Visual Studio Code avec les extensions Java fonctionnelles
- JDK récent (minimum JDK 13)

## Conception d'une interface graphique avec JavaFX

### Création de projet JavaFX sous Maven (pour **VS Code** uniquement)

- Ouvrez VS Code ; aucun projet ne doit être chargé
- Palette de Commande (_Ctrl+Shift+P_) -> "_Create Maven Project_"
- "_More..._"
- Recherchez "javafx" et sélectionnez "javafx-archetype-fxml" de _org.openjfx_
- Choisir la version la plus récente proposée
- Dans la fenêtre qui s'ouvre, sélectionnez le dossier contenant vos projets Java (un nouveau répertoire de projet y sera créé)
- group-id : _fr.dampierre_ (ou un autre nom de domaine fictif inversé, pas de majuscules, pas d'espaces)
- artefact-id : _projetjavafx_ (ou votre nom de projet, pas de majuscules, pas d'espaces)
- dans le terminal qui s'ouvre, validez la version 1.0 (_Define value for property 'version'_) en tapant "Entrée"
- package : (tapez "Entrée" si demandé)
- Confirmez par Y
- BUILD SUCCESS ! (Non ? Vérifiez le JDK installé, et la variable d'environnement utilisateur `JAVA_HOME`)
- VS Code vous propose d'ouvrir le projet nouvellement créé (sinon, ouvrez-le manuellement)

### Lancement de l'application

- Ouvrez le fichier `App.java` (dans `src`) et lancez l'application (_F5_) pour vous assurer de son bon fonctionnement
  - une fenêtre s'ouvre, contenant un label (_Primary View_) et un bouton unique (_Switch to Secondary View_)
  - appuyez sur le bouton
  - la fenêtre est remplacée par la _Secondary View_ et vous propose de repasser à la _Primary View_
- Cette petite application-démo ne fait rien d'autre que d'alterner entre deux vues, mais fixe les bases de fonctionnement d'une application JavaFX

### _Scene Builder_

- **_Scene Builder_** (SB) est une application indépendante de tout IDE qui permet de faciliter la réalisation d'interfaces graphiques (GUI) JavaFX
- Recherchez l'application _Scene Builder_ (https://gluonhq.com/products/scene-builder/) et installez-la
- Dans SB, on manipule des fichiers `.fxml`, pour créer et modifier des fichiers FXML contenant les vues (« écrans ») qui seront ensuite affichées par votre application JavaFX
- **Erreur fréquente** : SB ne vous rappelle pas de sauvegarder ; il arrive que l'on relance l'application sous VS Code après avoir modifié une vue FXML sous SB et que l'on se demande pourquoi ça ne fonctionne pas...

### Installation d'extensions VS Code

Avant d'aller plus loin, installez ces deux extensions pratiques sous VS Code (panneau « Extensions » sur la gauche) :

- `JavaFX Support` : permet d'éviter quelques avertissements (_warnings_) issus de bugs dans VS Code
- `SceneBuilder extension for Visual Studio Code` : permet simplement d'ouvrir par clic-droit un fichier FXML directement dans Scene Builder

### Ouverture d'une vue sous Scene Builder

- Sous VS Code, localisez et ouvrez le fichier `primary.fxml` dans le répertoire `resources`
- Ce fichier représente donc, sous forme de code FXML, l'interface graphique que vous voyez lorque l'application est lancée (la _Primary View_)
- Le format FXML a une structure hiérarchisée de type _markup_ (comme HTML, c'est un dérivé de XML)
- En général, on n'édite pas directement du code FXML (même si c'est tout à fait possible) : on utilise Scene Builder qui va permettre de modifier l'interface de manière beaucoup plus visuelle et intuitive
- Faites un clic-droit sur `primary.fxml` et sélectionnez _Open in Scene Builder_
- SB s'ouvre en chargeant le fichier concerné
- L'interface graphique de la vue `primary.fxml` s'affiche au milieu de l'application

### Fonctionnement de Scene Builder

- Quatre grandes zones à différencier :
  - au centre : l'interface graphique sur laquelle on travaille
  - en haut à gauche (_Library_) : la bibliothèque de ***controls***, qui sont les éléments graphiques (label, bouton, liste déroulante...)
  - en bas à gauche : la hiérarchie, qui retranscrit tous les _controls_ qui forment actuellement l'interface, sous forme d'arborescence
   - certains _controls_, comme la `VBox`, sont des « conteneurs » qui peuvent contenir d'autres _controls_ (voir _Layout et hiérarchie_, plus bas)
   - par exemple, ici, la `VBox` est une « boîte verticale » qui permet d'empiler les _controls_ les uns en dessous des autres
   - la `VBox` contient deux _controls_ :
    - un `Label` qui permet d'afficher le texte _Primary View_
    - un `Button` qui permettra de changer de vue
  - à droite (_Inspector_) : notamment les propriétés du _control_ actuellement sélectionné ; c'est là qu'on va modifier le texte d'un label, les dimensions d'un bouton, appliquer un effet, etc. (beaucoup de choses sont possibles pour chaque _control_)
- Le processus d'ajout de _control_ à l'interface consiste donc à :
  - localiser l'élément souhaité dans la _library_
  - le glisser-déposer directement dans l'interface graphique (ou dans la zone _hierarchy_, ce qui est parfois plus pratique)
  - modifier ses propriétés (texte, couleurs, marges...) dans le panneau _Inspector_

### Modification de l'interface

On va s'assurer que tout est bien en place en modifiant légèrement l'interface :

- Ajoutez un `Label` à la `VBox`
- Modifiez ses propriétés pour avoir le texte "Nouveau label" et une couleur de texte bleue
- Enregistrez le fichier FXML (_Ctrl-S_)
- Revenez sous VS Code et relancez l'application
- Vous devez voir votre nouveau label s'afficher sur la _Primary View_, mais pas sur la _Secondary View_, qui n'a pas été modifiée
  - si ce n'est pas le cas, vérifiez que vous avez bien sauvegardé le FXML et que vous travaillez sur le bon fichier

## Architecture de JavaFX

- Tout tourne autour de l'interaction entre les fichiers .java (logique de l'application, code métier, édités sous VS Code) et les fichiers FXML (qui contiennent les interfaces graphiques, édités sous SB)
- Dans une application JavaFX :
  - on dispose d'un objet `Stage` (c'est la fenêtre principale) fourni par le _runtime_ Java
  - le `Stage` contient un objet `Scene` (contenu de la fenêtre, qu'on va pouvoir changer au cours de l'application)
  - la `Scene` contient une `root` (racine) : c'est un fichier FXML qui décrit l'interface graphique
- L'idée est donc :
  - de créer sous SB autant de fichiers FXML qu'il y a de vues dans l'application,
  - de peupler la fenêtre (`Scene`) avec le fichier FXML d'accueil
  - de réagir dans le code Java aux événements qui sont détectés dans l'interface (clic sur un bouton, appui sur une touche...)
  - tout en changeant de vue (la _root_) lorque nécessaire

### Étude du code de l'application-démo

Étudions le code de la classe `App` :

```java
public class App extends Application {

  private static Scene scene;

  @Override
  public void start(Stage stage) throws IOException {
    scene = new Scene(loadFXML("primary"), 640, 480);
    stage.setScene(scene);
    stage.show();
  }

  static void setRoot(String fxml) throws IOException {
    scene.setRoot(loadFXML(fxml));
  }

  private static Parent loadFXML(String fxml) throws IOException {
    FXMLLoader fxmlLoader = new FXMLLoader(App.class.getResource(fxml + ".fxml"));
    return fxmlLoader.load();
  }

  public static void main(String[] args) {
    launch();
  }
}
```

- (Ignorez le « bruit » que représentent les `...extends Application`, `...throws IOException`, `@Override`...)
- Cette classe dispose de 4 méthodes
  - la méthode `main` (point de départ du programme) se contente d'appeler la méthode `launch` de JavaFX
  - la méthode `launch`, dont on ne voit pas la définition ici, va en fait appeler elle-même la méthode `start`, que l'on peut considérer comme le point de départ fonctionnel du programme
  - la méthode `start`
   - crée une `Scene` (`new Scene`) de 640x480 pixels en y chargeant la vue `primary.fxml`
   - indique au `Stage` que c'est la `Scene` qu'il faut utiliser (`setScene`)
   - et enfin l'affiche à l'écran (`show`)
  - la méthode `loadFXML` charge une vue FXML depuis un nom de fichier passé en paramètre (`String fxml`) et renvoie la vue sous forme utilisable (`Parent`)
  - la méthode `setRoot` permet de passer à la vue donnée en paramètre (`String fxml`)

## _Layout_ (dispositon des _controls_) et hiérarchie

- Pour concevoir une interface graphique en JavaFX, il faut raisonner en terme de d'éléments conteneurs qui contiendront d'autres éléments
- Il y a donc une hiérarchie depuis la racine (_root_) qui est très souvent un conteneur
- Les conteneurs peuvent contenir récursivement d'autres containers, et ainsi de suite, sans limite de profondeur ; cela permet de concevoir des écrans potentiellement très complexes
- Par exemple, on pourra avoir :
  - un conteneur `VBox` (layout vertical)
  - qui contiendra lui-même :
   - un `Label` pour afficher un titre
   - une `ListView` pour afficher une liste de clients
   - un `TextField` (champ texte éditable) qui permettra de rechercher un client par son nom
   - un conteneur `HBox` (layout horizontal)
    - qui lui-même contiendra plusieurs boutons empilés horizontalement

## Les conteneurs

Le panneau _Library_ contient plusieurs catégories de _controls_, dont les conteneurs. Chaque conteneur disponible est spécialisé pour une certaine disposition des éléments qu'il contient. Les sections suivantes en présentent quelques-uns.

### StackPane

- Empile les _controls_ les uns sur les autres, au centre
- En général on ne veut pas cela car les éléments sont cachés les uns derrière les autres

### AnchorPane

- Permet de « scotcher » (ancrer) les éléments par rapport au 4 bords du _container_
- Ainsi, quand on redimensionne, l'élément reste « ancré » par rapport aux bords désignés
- Souvent utilisé comme conteneur racine pour contrôler les marges

### GridPane

- Définit une grille _n x m_ dans laquelle on place les _controls_ sur _n_ lignes et _m_ colonnes
- Un _control_ pourra s'étendre sur plusieurs lignes et/ou colonnes, si besoin
- Conteneur très pratique, par exemple pour ranger trois lignes de couples `Label+TextField` (formulaire classique), on pourra utiliser une `GridPane` de 3x2

### FlowPane et TilePane

- Permet de définir des _controls_ les uns à côté des autres (ou les uns en dessous des autres)
- S'adapte à la taille de la fenêtre, dans le sens où les _controls_ « passeront à la ligne » si la place n'est pas suffisante

### BorderPane

- Permet de créer un layout avec cinq sections : haut, bas, gauche, droite, centre (potentiellement vides)
- Chaque section est elle-même un conteneur pouvant contenir d'autres éléments
- C'est ainsi qu'est définie l'interface de SB, par exemple, avec ses panneaux sur les côtés

### SplitPane

- Permet de diviser l'espace en deux parties redimensionnables horizontalement ou verticalement
- Par exemple, le panneau gauche de VS Code est redimensionnable en faisant glisser le bord du panneau
- Typiquement, les deux zones d'un `SplitPane` contiennent un autre conteneur
- Un `SplitPane` peut contenir un autre `SplitPane`, etc. On peut ainsi construire un layout arbitrairement complexe dont chaque partie est redimensionnable

### HBox, VBox, ButtonBar

- `HBox` : placement horizontal
- `VBox` : placement vertical
- `ButtonBar` : spécialisé dans le placement horizontal de boutons

## Les controllers

On va vouloir réagir dans 

- Quand vous donnez un fichier FXML comme racine d'une _Scene_, le FXML est analysé et transformé en objets Java qui vont pouvoir être manipulés dans le code (accès en lecture/écriture à telle zone de texte, peupler une liste, réaction à un événement...)
- Pour cela, en FXML sous SB, on donne des noms à chaque élément que l'on va vouloir manipuler (sous-panneau _Code_ de _Inspector_, propriété `fx:id`)
- Dans le _controller_, on aura alors accès à cet élément en le désignant par son nom

### Configurer les actions

- Des événements, auxquels vous pouvez réagir, sont définis sur chaque _control_
  - clic sur un bouton
  - appui sur touches du clavier
  - passer la souris au-dessus d'un élément...
- On peut définir des méthodes, appelées _handlers_, qui définissent ce qui doit être fait lorsque l'événement survient
- On relie un événement à une méthode _handler_ par l'intermédiaire du _controller_ (voir plus loin)

### Exemple de _controller_

- On va reprendre comme base le `PrimaryController` défini dans l'application-demo, comprendre comment il fonctionne et le modifier
- Dans SB, ouvrez `primary.fxml`, situé dans un sous-répertoire de `resources`
- Notez la structure aborescente du code FXML ; cependant, en général, vous n'allez jamais éditer un fichier FXML directement, même si il arrive de les consulter pour chercher à expliquer une erreur
- Utilisez le clic-droit pour l'ouvrir sous SB
- Dans SB, ouvrez le sous-panneau _controller_ (tout en bas à gauche)
  - notez que le champ `Controller class` est défini
  - cela signifie qu'un _controller_ est relié à cette _view_
  - c'est le fichier `PrimaryController` que l'on retrouve dans notre projet
  - il est complètement qualifié, c'est-à-dire qu'il est précédé du nom de son package (`fr.votredomaine`)
  - quand vous définissez une vue, **vous devez toujours définir le _controller_ associé**
- Sélectionnez maintenant le bouton _Switch to Secondary View_
- Dans le panneau _Inspector_, sous-panneau *Code* :
  - localisez `fx:id` (_identity_)
  - notez que le champ est déjà renseigné avec le nom `primaryButton`  : c'est le nom du bouton
  - localiser `On Action`
  - notez que le champ est déjà renseigné avec `switchToSecondary` : c'est le nom de la méthode qui va être associée à l'action principale de cet élément (clic)
- Allez dans le menu _View/Show Sample Controller Skeleton_
  - cela montre un exemple de code _controller_
  - notez qu'il définit une variables pour l'élément auquel on a donné un nom
  - et une méthode vide dont le nom correspond au nom donné plus haut
  - lorsque l'on définit de nouveaux noms/actions, on peut utiliser cet exemple de code pour copier/coller les nouvelles parties dans le _controller_ sous VS Code avant de définir le code des méthodes
- Revenez sous VS Code et observez de nouveau le code de `PrimaryController`
  - notez que le nom du bouton n'a pas été conservé (le code ne l'utilise pas) ; s'il était défini, on pourrait accéder aux propriétés du bouton dans le code en utilisant la notation pointée (par exemple `primaryButton.setTextFill(Color.web("BLUE"))` changera le texte en bleu)
  - l'entête de la méthode change un peu par rapport au code-exemple de SB mais cela revient au même
  - la méthode est implémentée : elle fournit le code associé à l'événement
  - ici on vient, en appelant `setRoot()` dans la classe `App`, changer la racine de la `Scene`, ce qui résulte en l'affichage du second écran (`secondary.fxml`)

### Testez par vous-même

- Dans `secondary.fxml`, faire en sorte que, lorsque l'on clique sur le bouton :
  - la couleur du texte du bouton passe en rouge
  - le texte du label du dessus se change en "COUCOU !"
  - (consultez la section plus bas pour les détails si vous n'y arrivez pas)

### N'oubliez pas

- Quand vous définissez une nouvelle vue (FXML), vous devez :
  - définir un nouveau fichier _controller_ dans VS Code
  - sous SB, associer la vue avec ce _controller_
  - pour chaque élément auquel on voudra accéder, lui donner un nom
  - pour chaque événement auquel on voudra réagir, renseigner le nom de méthode correspondante sur le _control_ associé
  - utiliser SB pour vous indiquer à quoi doit ressembler le code de _controller_
  - utiliser la notation pointée pour accéder aux propriétés des _controls_ (en lecture ou en écriture)

## Détails de l'implémentation d'un nouvel écran

Voici donc les étapes à considérer lorque vous concevez un nouvel écran :

- Partir d'un fichier .fxml existant (en le copiant) ou bien en créant un fichier .fxml vierge sous SB
  - rappel : les fichiers .fxml doivent être enregistrés dans un sous-répertoire (correspondant au nom de votre package) du répertoire `resources` de votre projet pour que Java les trouvent (par exemple `mon-projet\src\main\resources\fr\pgah\Connexion.fxml`)
- Donner un nom expressif à ce fichier .fxml
  - (donner un nom expressif à tout ce qu'on peut nommer est (très) important en programmation)
- Créer l'interface graphique en glissant-déposant les _controls_ dont vous avez besoin
- Utiliser les panneaux _Proprerties_ et _Layout_ de droite pour adapter l'élément à vos besoins (texte affiché, couleur, taille... en fonction de la nature de l'élément)
- Utiliser le troisième panneau _Code_ de droite pour :
  - donner un nom à l'élément grâce à l'attribut `fx:id` (uniquement si vous avez besoin d'y accéder depuis le code Java par la suite, par exemple pour récupérer le contenu d'un _textfield_)
  - indiquer un nom de méthode qui se produira lorsque l'élément sera « actionné » grâce à l'attribut `On Action` ou un autre désignant l'événement (uniquement si vous voulez réagir à une action sur cet élément, le plus souvent pour un clic de bouton)
- Quand vous avez un écran suffisamment rempli pour la mise en place d'au moins une fonctionnalité, il est temps de passer à la logique côté Java sous VS Code, pour coder le _controller_ qui va correspondre à cette vue
- Mais d'abord, pour se faciliter la tâche, on va demander à SB de nous montrer à quoi devra ressembler le code du _controller_ pour qu'il prenne en compte tous les éléments que l'on a nommés et les méthodes que l'on a mises en place
  - menu `View/Show Sample Controller Skeleton`
  - copier le code du _controller_ présenté
  - voici un exemple avec un champ texte nommé `txtPrenom` et un bouton nommé `btnValider` ; on a également indiqué qu'un clic sur ce bouton lance la méthode `btnValiderClic`

```java
package fr.pgah;

import javafx.event.ActionEvent;
import javafx.fxml.FXML;
import javafx.scene.control.TextField;
import javafx.scene.control.Button;

public class TestController {

  @FXML
  private TextField txtPrenom;

  @FXML
  private Button btnValider;

  @FXML
  void btnValiderClic(ActionEvent event) {
  }
}
```

- Notez la façon dont les éléments graphiques sont nommés : un préfixe indique de quel type d'élément il s'agit
  - `txt` pour un champ texte, `btn` pour un bouton, etc.
  - ce n'est pas obligatoire mais c'est une bonne convention
- Sous VS Code, créer un nouveau fichier aux côté du fichier `App.java`, dans le répertoire principal de votre package
  - même nom que pour le fichier .fxml, avec le suffixe `Controller` (ex: `ConnexionController.java`)
  - y coller le code du « squelette » donné par SB
- N'oubliez pas que **chaque variable et chaque méthode déclarée en FXML (depuis SB) doit avoir l'annotation `@FXML`** sinon Java ne considérera pas que les deux sont reliés (mettre plusieurs déclarations de variables sous une seule annotation `FXML` n'est pas suffisant)
- Pour relier effectivement le fichier FXML avec ce _controller_, retourner dans SB
  - panneau _Controller_, en bas à gauche
  - indiquer le nom complet de la classe _controller_ nouvellement définie
  - conseil : utiliser le _dropdown_ pour être sûr de ne pas se tromper
- Il faut maintenant implémenter les méthodes d'action pour effectuer les traitements correspondants
- Souvent, on a besoin de récupérer des informations depuis l'interface graphique pour effectuer le traitement
  - ex : récupérer le contenu d'un champ texte
  - il faut « interroger » l'objet correspondant
  - ex : `txtPrenom.getText()` retourne le contenu du champ texte
  - on peut ensuite utiliser cette donnée dans un traitement quelconque :

```java
@FXML
void btnValiderClic(ActionEvent event) {
  String lePrenom = txtPrenom.getText();
  // Affichage sur la console pour vérification
  System.out.println("Prénom récupéré :" + lePrenom);
  // Puis on peut utiliser lePrenom dans une requête SQL
  // Code de connexion BDD non reproduit...

  // Préparation de la requête
  String req = "SELECT * FROM Users WHERE prenom='" + lePrenom + "'";
  Statement statement = conn.createStatement();
  // Exécution de la requête
  ResultSet result = statement.executeQuery(req);
  // On boucle pour traiter tous les résultats
  while (result.next()){
    // Récup du num et de l'email depuis cet enregistrement
    String nom = result.getString("nom");
    String email = result.getString("email");
    // Simple affichage dans la console de sortie
    System.out.println("Nom : " + nom + " ; email : " + email));
  }
}
```

- Les `println` sont utiles pour suivre l'avancée des opérations et vérifier que les données récupérées sont cohérentes, mais on va aussi vouloir mettre à jour l'écran JavaFX avec ces données
- Il faut de nouveau aller interroger les objets qui correspondent aux éléments à mettre à jour pour savoir comment les modifier
  - une façon d'explorer est de taper `txtPrenom.` dans l'IDE : VS Code va nous montrer toutes les méthodes pouvant être appelées depuis cet objet
  - on peut aussi [se renseigner sur Internet](http://tutorials.jenkov.com/javafx/textfield.html) sur l'usage du _control_ JavaFX en question
  - par exemple, pour afficher dans un `TextField` une informations d'un employé dont a a récupéré l'id :

```java
@FXML
void btnValiderClic(ActionEvent event) {
  // Récupération de l'id depuis un champ texte
  int num = txtNumEmploye.getText();
  // Code de connexion BDD non reproduit...
  // Préparation de la requête
  String req = "SELECT prenom FROM Employes WHERE id='" + num + "'";
  Statement statement = conn.createStatement();
  // Exécution de la requête
  ResultSet result = statement.executeQuery(req);
  // Cette fois on n'a qu'un seul résultat (au plus)
  // puisqu'on a filtré sur la clé primaire
  // On teste pour savoir si on a effectivement un résultat
  if (rs.next())
  {
    // Récup du prénom depuis le résultat de la requête
    String prenom = rs.getString("prenom");
    // Mise à jour du champ texte JavaFX avec setText
    txtPrenom.setText(prenom);
  }
}
```


























## Accès à une base de données via JDBC

### JDBC

- JDBC (_Java Database Connectivity_) est une interface de programmation Java qui permet aux applications d'accéder à une base de données relationnelle
- Des pilotes JDBC sont disponibles pour tous les systèmes connus de bases de données relationnelles, comme MySQL
- Pour pouvoir utiliser facilement JDBC, votre projet de départ doit être généré par Maven
- Dans votre projet généré par Maven :
  - ouvrez la palette de commande
  - tapez `maven`
  - sélectionnez _Add a dependency_
  - trouvez `mysql-connector-java`
  - la dépendance devrait être ajoutée au fichier `pom.xml` :

```
<dependencies>
    ...
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>X.Y.Z</version>
    </dependency>
    ...
</dependencies>
```

- Si votre projet dispose d'un fichier `module-info.java` (s'il s'agit d'un projet javafx notamment), modifiez-le pour ajouter `java.sql` (en ne touchant surtout pas au reste du fichier) :

```java
module fr... {
  // requires...
  requires java.sql;
	// opens...
	// exports...
}
```

- Votre projet est maintenant configuré pour reconnaître du code JDBC d'accès à une BDD
- Consultez le lien suivant pour ensuite accéder à MySQL à partir de code Java : [Tuto indicatif pour l'utilisation de classes JDBC](https://www.codejava.net/java-se/jdbc/jdbc-tutorial-sql-insert-select-update-and-delete-examples)
- Attention, dans la suite, lorsque vous résolvez les imports d'objets SQL manquants (avec la petite ampoule ou bien `Ctrl+.`), sélectionnez le package `java.sql`
- **Partie 1** : à ignorer, vous devez déjà avoir une installation Java et MySQL correcte. Assurez-vous de bien relever les informations suivantes concernant la configuration du SGBRD (elles seront bien sûr nécessaires pour assurer la connexion Java/MySQL) : port, identifiant utilisateur, mot de passe, nom de la BDD
- **Partie 2** : dans l'idéal, utilisez immédiatement la BDD correspondante à ce que vous essayez de faire. Sinon, n'importe quelle petite table, comme celle qui est présentée, fera l'affaire pour tester
- **Partie 3** : Lisez (même si vous ne comprenez pas bien) cette partie décrivant les classes qui vont être utilisées. Essayez par la suite de vous y rapporter régulièrement pour comprendre ce qui se passe au fur et à mesure. Repérez les appels de méthodes statiques (directement sur une classe - Majuscule) et les appels de méthodes d'instances (sur des variables objets - minuscule)
- **Partie 4** : premier objectif => une connexion réussie à la BDD via Java (le message doit s'afficher dans la console). Notez que la connexion à la BDD est encapsulée dans un block `try...catch` : c'est une construction Java qui permet de capturer les erreurs éventuelles qui peuvent se produire lors de la connexion et permettent de récupérer le contrôle du flux d'exécution (au lieu d'avoir un programme qui se termine de manière abrupte par un message d'erreur)
- **Parties 5/6/7/8** : CRUD que vous adapterez à votre application. Chaque fonctionnalité de l'application sera modularisée dans sa (ses) propre(s) méthode(s). La connexion à la BDD, répétée à chaque requête, sera également encapsulée dans une méthode dédiée pour éviter la duplication de code
- Une fois le CRUD opérationnel en ligne de commande, on pourra s'occuper de construire une interface graphique avec JavaFX conjugué à *Scene Builder* ; les méthodes réagissant aux événements s'occuperont de la logique métier et appelleront les méthodes d'accès à la BDD quand elles en auront besoin