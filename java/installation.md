# Mise en place de l'environnement

Pour développer en Java, vous aurez besoin de :

- un Environnement de Dévelopement Intégré (IDE) ; nous utiliserons Visual Studio Code
- Java Development Kit (JDK)
- ensemble d'outils Java pour l'IDE

## Préparation

Pour éviter d'avoir des problèmes de compatibilité, il faut auparavant désinstaller toutes les versions précédentes du JDK qui pourraient être installées sur votre système.

### Suppression des JDK

- rendez-vous dans les paramètres de Windows
- *Applications*
- recherchez « jdk » dans la liste de programmes installés
- supprimez tous les jdk trouvés

### Suppression des entrées dans les variables d'environnement

La variable d'environnement PATH sur votre système contient un ensemble de répertoires qui sont parcourus lorsque le système tente de localiser un programme. Il se peut que les JDK désinstallés aient posé des entrées dans cette variable qui n'ont pas été supprimées. Il est important de les supprimer pour éviter tout problème d'incompatibilité par la suite. Il est tout à fait possible et même probable que vous ne trouviez rien à supprimer du tout. Il faut quand même vérifier :

- rendez-vous dans les paramètres de Windows
- dans la recherche de paramètres, tapez « environ », localisez et ouvrez la fenêtre de consultation des variables d'environnement
- dans la liste des entrées « **variables utilisateur** » :
  - **ATTENTION : dans ce qui suit, ne supprimez surtout pas l'ensemble de la variable PATH**
  - localisez la variable PATH (si elle existe)
  - modifiez-la (bouton) ; une liste de chemin s'affiche
  - vérifiez dans la liste des chemins si certains contiennent une référence à un JDK (ils contiendront la chaîne de caractères « jdk »)
  - supprimez-les tous le cas échéant
- toujours dans la liste des entrées « variables utilisateur » :
  - localisez la variable JAVA_HOME (si elle existe)
  - supprimez la variable complètement
- dans la liste des entrées « **variables système** » :
  - répétez le processus précédent pour les chemins contenus dans la variable PATH
  - répétez le processus précédent pour la variable JAVA_HOME (si elle existe)

Par exemple, sur le système suivant, ces trois entrées doivent être considérées :

![variables d'environnement](assets/variables_environnement_java.png)

Le système est maintenant prêt à accueillir un nouveau JDK.

## Visual Studio Code (VS Code)

Nous allons installer un _bundle_ (ensemble logiciel) pour Windows qui comprend tout ce dont on a besoin. Téléchargez et installez l'application suivante :

- [pour Windows](https://aka.ms/vscode-java-installer-win)
- [pour macOS](https://aka.ms/vscode-java-installer-mac)
- sous Linux, il faut faire l'installation « manuellement » (JDK + VS Code + extensions Java pour VS Code)

Pour terminer l'installation, il faut se **déconnecter du système et se reconnecter** (le redémarrage complet de la machine n'est cependant pas nécessaire).

NB : à la première ouverture de VS Code, on vous propose l'installation d'un pack linguistique pour le français. Il est déconseillé d'installer ce pack : l'utilisation d'un IDE en anglais vous apprendra les termes que vous retrouverez plus tard dans la documentation en anglais. Dans le cas général, en informatique, on doit être à l'aise avec la lecture de sources de documentation en anglais et avec les logiciels en anglais, sans traduction automatique. Travailler directement en anglais vous épargnera de nombreux problèmes et vous facilitera globalement votre futur métier.

## Créer un projet Java

- une fois reconnecté, ouvrez VS Code
- tapez`Ctrl+Shift+P` (`Shift` = `Maj` = touche avec une flèche au-dessus de `Ctrl`)
- la **palette de commande** s'ouvre : c'est un outil très utile sous VS Code qui permet d'accéder à toutes les fonctionnalités par simple recherche
- tapez `java`
- localisez et lancez `Create Java Project` dans la liste qui s'affiche
- sélectionnez `Maven` (si pas disponible, l'installation n'est pas correcte)
- tapez `junit5` dans le champ de recherche
- aucune proposition correspondante n'apparaît dans la liste, mais cliquez sur `More...`
- sélectionnez `java11-junit5`
- sélectionnez la dernière version disponible
- pour le nom du *package*, la convention généralement utilisée est de mettre le nom de domaine *inversé* de l'organisation (par exemple : `fr.dampierre`)
- pour l'*artifact*, tapez le nom de votre projet (par exemple `introjava`)
- le système ouvre une fenêtre pour vous laisser choisir le répertoire dans lequel sera stocké votre nouveau projet
- parcourez l'arborescence pour localiser votre répertoire de projets Java (par exemple, vous pourriez avoir un répertoire `Java` sur votre bureau Windows)
- **Attention** : ne créez pas un répertoire spécifique pour le nouveau projet (Maven va le faire pour vous) ; indiquez juste votre répertoire de projets Java
- la suite se passe dans le terminal qui s'ouvre dans la partie inférieure de VS Code ; la création de projet est lancée
- la première fois, le gestionnaire de dépendances **Maven** va faire quelques téléchargements : une connexion internet est donc nécessaire pour cette phase
- au bout d'un moment, le processus va se stopper pour vous laisser indiquer le numéro de version de base de votre programme : laissé le numéro proposé (1.0-SNAPSHOT) et appuyez sur `Entrée` (il faudra peut-être donner le focus au terminal en cliquant dessus avant)
- confirmez le résumé donné avec `Entrée`
- le projet est créé ; cliquez sur `Open` dans la popup qui s'ouvre ; VS Code se relance et le nouveau projet est chargé
- Indiquez que vous « faites confiance » aux auteurs des fichiers ouverts (il peut être prudent de ne pas « faire confiance » à du code quelconque téléchargé sur Internet : cela vous permettra d'examiner le programme sans pouvoir l'exécuter, car il pourrait contenir du code malicieux)
- laissez toujours quelques secondes à VS Code pour charger le projet en arrière-plan
- **par la suite, lorsque vous ouvrirez de nouveau un projet existant (`File / Open Folder...`), veillez à toujours bien sélectionner le répertoire contenant le projet, et non pas un répertoire plus haut ou bien un répertoire plus bas** ; il faut toujours qu'un projet Java ouvert indique une architecture de répertoire comme ceci sur le panneau `Explorer` :

![architecture_repertoires_java](assets/architecture_repertoires_java.png)

### Ça ne fonctionne pas ?

- Vérifiez votre accès Internet
- Vérifiez que vous vous êtes bien déconnecté/reconnecté après l'installation de VS Code
- Vérifiez que vous disposez de la variable d'environnement `JAVA_HOME` qui pointe vers le répertoire du JDK installé (sinon, l'ajouter)
- Vérifiez que votre `PATH` contient également le chemin vers ce même JDK (sinon, l'ajouter)
- Vérifiez que vous n'avez pas d'anciens `JAVA_HOME` ou des répertoires dans les variables `PATH` qui pointeraient vers des répertoires inexistants ou d'anciens JDK, supposés désinstallés ; normalement, vous devriez avoir :
  - une variable `JAVA_HOME` dans les variables d'environnement utilisateur
  - le répertoire pointant vers votre JDK fraîchement installé dans la variable d'environnement utilisateur `PATH`

## Lancement du programme

- Le programme se lance avec l'appui sur la touche `F5` du clavier (il se peut que vous deviez utiliser conjointement la touche `Fn` de votre laptop)
- Au premier lancement, le parefeu de Windows vous demandera à quels réseaux doit avoir accès VS Code ; cochez les réseaux privés, mais pas les réseaux publics
- Notez que le programme, tel qu'il est construit ici, ne fait absolument rien ; vérifiez juste que vous n'avez pas d'erreurs affichées dans le terminal
