# Mise en place de l'environnement

Pour développer en Java, vous aurez besoin de :

- un Environnement de Dévelopement Intégré (IDE) ; nous utiliserons Visual Studio Code
- Java Development Kit (JDK)
- ensemble d'outils Java pour l'IDE

## Préparation

Pour éviter d'avoir des problèmes de compatibilité, il faut auparavant désinstaller toutes les versions précédentes du JDK qui pourraient être installées sur votre système.

### Suppression des JDK

- rendez-vous dans les paramètres de Windows
- Apps
- recherchez « jdk » dans la liste de programmes installés
- supprimez tous les jdk trouvés

### Suppression des entrées dans les variables d'environnement

La variable d'environnement PATH sur votre système contient un ensemble de répertoires qui sont parcourus lorsque le système tente de localiser un programme. Il se peut que les JDK désinstallés aient posé des entrées dans cette variable qui n'ont pas été supprimées. Il est important de les supprimer pour éviter tout problème d'incompatibilité par la suite. On va donc vérifier manuellement :

- rendez-vous dans les paramètres de Windows
- dans la recherche de paramètres, tapez « environ », localisez et ouvrez la fenêtre d'édition des variables d'environnement
- dans la liste des entrées « **variables utilisateur** » :
  - **ATTENTION : dans ce qui suit, ne supprimez surtout pas l'ensemble de la variable PATH**
  - localisez la variable PATH (si elle existe)
  - éditez-la (bouton) ; une liste de chemin s'affiche
  - vérifiez dans la liste des chemins si certains contiennent une référence à un JDK (ils contiendront la chaîne de caractères « jdk »)
  - supprimez-les tous le cas échéant
- toujours dans la liste des entrées « variables utilisateur » :
  - localisez la variable JAVA_HOME (si elle existe)
  - supprimez la variable complètement
- dans la liste des entrées « **variables système** » :
  - répétez le processus précédent pour les chemins contenus dans la variable PATH
  - répétez le processus précédent pour la variable JAVA_HOME (si elle existe)

Par exemple, sur le système suivant, ces trois entrées doivent être considérées :

![variables d'environnement](assets/variables_environnement.png)

Le système est maintenant prêt à accueillir un nouveau JDK.

## Visual Studio Code

Nous allons installer un _bundle_ (ensemble logiciel) pour Windows qui comprend tout ce dont on a besoin. Téléchargez et installez l'application suivante :

- [pour Windows](https://aka.ms/vscode-java-installer-win)
- [pour macOS](https://aka.ms/vscode-java-installer-mac)
- sous Linux, il faut faire l'installation « manuellement »


