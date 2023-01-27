# TP IMC

## Introduction

Le but de cet exercice est de créer des « patients » qui ont un poids et une taille, et de calculer leur « Indice de Masse Corporelle » (IMC).

## Description de la solution

Créez un nouveau projet Java (_imc_) et faire en sorte que la méthode _main_ de la classe principale soit comme il suit :

```java
// Méthode main initiale
// Vous ne devez pas modifier cette méthode
public static void main(String[] args) {
    Patient patient = new Patient(74.5, 1.75);
    System.out.println(patient.caractéristiques());
    System.out.println("IMC exact : " + patient.calculerIMC());
    Patient autrePatient = new Patient( -2.0, 4.5);
    System.out.println(autrePatient.caractéristiques());
}
```

Le code fourni crée un patient et affiche les données du patient ainsi que son IMC.
Ces deux étapes sont répétées deux fois avec des valeurs différentes.
Le code fourni n'est pas compilable car la classe _Patient_ n'est pas fournie. Il vous est demandé de l'implémenter.

Un patient est caractérisé par un poids et une taille. Les méthodes spécifiques à un patient sont :

- un constructeur prenant en paramètre deux _double_, le premier pour
  initialiser le poids du patient et le second pour initialiser sa taille ; ces données ne seront affectées aux attributs du patient que si elles sont toutes les deux positives ; dans le cas contraire, la taille et le poids du patient seront tous deux initialisés à zéro ; pour simplifier, il n'y a pas d'autre contrôle à faire sur ces données

— une méthode `caractéristiques` : renvoie une `String` contenant les caractéristiques du patient en respectant strictement le format suivant : `Patient : <poids> kg pour <taille> m (IMC : <imc>)` où `<poids>`, `<taille>` et `<imc>` sont à remplacer par leurs valeurs respectives ; on arrondira le poids et la taille à un chiffre après la virgule ; l'IMC sera calculé à partir de la méthode `calculerIMC` puis arrondi à deux chiffres après la virgule

- une méthode `calculerIMC` : renvoie l'IMC du patient (son poids divisé par sa taille au carré) sous forme de _double_ avec le maximum de précision (pas d'arrondi) ; en cas de taille nulle, cette méthode renvoie zéro (on ne peut pas diviser par zéro, cela produirait une exception qui ferait « crasher » le programme)

## Exemple d'exécution

Après implémentation de la classe _Patient_, la méthode _main_ donnée dans la section précédente produira la sortie suivante (notez les nombres arrondis) :

```
Patient : 74,5 kg pour 1,8 m (IMC : 24,33)
IMC exact : 24.3265306122449
Patient : 0,0 kg pour 0,0 m (IMC : 0,00)
```
