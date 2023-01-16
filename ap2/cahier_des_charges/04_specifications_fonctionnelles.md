# Spécifications fonctionnelles de l’application de gestion des frais

Ce document concerne les spécifications fonctionnelles de l'application « Gestion des frais ».

Cette application est destinée aux visiteurs médicaux et personnels du service comptable, les premiers pour renseigner et consulter leurs états de frais, les seconds pour réaliser le suivi des états de frais des visiteurs médicaux jusqu'à leur règlement.

## Cas d'utilisation

Les besoins sont exprimés ici à l'aide des cas d'utilisation : le diagramme des cas d'utilisation pour la vue synthétique de « qui fait quoi », puis une fiche par cas d'utilisation pour décrire les échanges entre le système et l'utilisateur.

## Diagramme des cas d'utilisation

![diagramme_ucs](/cahier_des_charges/diagramme_ucs.png)

## Les fiches des cas d'utilisation

### Cas d'utilisation 1

- Nom cas d’utilisation : Se connecter
- Acteur déclencheur : Visiteur médical ou Comptable
- Pré conditions : Néant
- Post conditions : L’utilisateur est reconnu visiteur médical ou comptable

- Scénario nominal :

1. Le système affiche un formulaire de connexion
2. L'utilisateur saisit son login et son mot de passe et valide
3. Le système contrôle les informations de connexion, informe que le profil Visiteur ou Comptable est activé, et maintient affichée l'identité du visiteur médical / comptable connecté.

- Exceptions :

  - 3a. : le nom et/ou le mot de passe n’est pas valide
    - 3-a.1 Le système en informe l’utilisateur ; retour à l'étape 1

- Contraintes : Néant

- Questions ouvertes : Néant

### Cas d'utilisation 2

- Nom cas d’utilisation : Renseigner fiche de frais
- Acteur déclencheur : Visiteur médical
- Pré conditions : Visiteur médical authentifié
- Post conditions : Néant

- Scénario nominal :

1. L’utilisateur demande à saisir un ou plusieurs frais pour le mois courant.
2. Le système retourne les frais actuellement saisis - éléments forfaitisés et hors forfait - pour le mois courant.
3. L’utilisateur ajoute ou modifie éventuellement une ou des valeurs des frais au forfait et demande la validation.
4. Le système enregistre cette ou ces modifications et retourne ces valeurs à jour.
5. L’utilisateur ajoute éventuellement un nouveau frais hors forfait en renseignant les différents champs (date d'engagement, libellé, montant) et valide.
6. Le système enregistre la ligne de frais hors forfait.

- Exceptions :

  - 2.a C’est la première saisie pour le mois courant. Si ce n’est pas encore fait, le système clôt la fiche du mois précédent et crée une nouvelle fiche de frais avec des valeurs initialisées à 0. Retour à 3.
  - 4.a. Une valeur modifiée n’est pas numérique : le système indique « Valeur numérique attendue ». Retour à 3.
  - 6.a Un des champs n'est pas renseigné : le système indique : « Le champ date (ou libellé ou montant) doit être renseigné ».
  - 6.b La date d'engagement des frais hors forfait est invalide : le système indique « La date d'engagement doit être valide ». Retour à 5.
  - 6.c La date d'engagement des frais hors forfait date de plus d’un an. Le système indique « La date d'engagement doit se situer dans l’année écoulée ». Retour à 5.
  - 7.1 L’utilisateur sélectionne un frais hors forfait pour suppression.
    - 7.2 Le système enregistre cette suppression après une demande de confirmation.

- Contraintes : Néant

### Cas d'utilisation 3

- Nom cas d’utilisation : Consulter mes fiches de frais
- Acteur déclencheur : Visiteur médical
- Pré conditions : Visiteur médical authentifié
- Post conditions : néant

- Scénario nominal :

1. L'utilisateur demande à consulter ses frais.
2. Le système invite à sélectionner un mois donné.
3. L'utilisateur sélectionne un mois donné, puis valide.
4. Le système affiche l'état de la fiche de frais avec la date associée, les éléments forfaitisés – quantité pour chaque type de frais forfaitisé - et non forfaitisés – montant, libellé et date d'engagement - existant pour la fiche de frais du mois demandé.

- Exceptions : néant si les recommandations ci-dessous sont appliquées

- Contraintes : néant

- Questions ouvertes :

La sélection d'un mois pourra être facilitée par l'IHM. Il est possible de proposer les mois pour lesquels le visiteur médical connecté dispose d'une fiche de frais. On pourra se restreindre à remonter jusqu'au début de l'année civile précédente. Cela évitera en amont la gestion d'erreurs lors de la sélection du mois (étape 3).

### Cas d'utilisation 4

- Nom cas d’utilisation : Valider fiche de frais
- Acteur déclencheur : Comptable
- Pré conditions :
  - Utilisateur Comptable authentifié
  - Toutes les fiches du mois qui vient de s’achever sont clôturées par un script
  - Le comptable dispose de tous les éléments pour évaluer la conformité des frais forfaitisés
- Post conditions : Néant

- Scénario nominal :

1. L’utilisateur demande à valider les fiches de frais
2. Le système propose de choisir le visiteur et le mois concernés
3. L’utilisateur sélectionne les informations et valide
4. Le système affiche le détail de la fiche de frais (frais forfaitisés et hors forfait)
5. L’utilisateur actualise les informations des frais forfaitisés.
6. Le système indique que la modification a été prise en compte et affiche les informations actualisées.
7. L’utilisateur demande la suppression des lignes de frais hors forfait non valides
8. Le système modifie le libellé en ajoutant en début le texte « REFUSÉ : ».
9. L'utilisateur valide la fiche.
10. Le système passe la fiche à l’état « Validée » et met à jour la date de modification de la fiche.

- Exceptions :

  - 4-a : Aucune fiche de frais n’existe, le système affiche « Pas de fiche de frais pour ce visiteur ce mois ». Retour au 2
  - 7.a : L'utilisateur demande le report des frais hors forfait pour lesquels une facture acquittée n’a pas été reçue dans les temps.
  - 8.a : Le système ajoute la ligne hors forfait dans la fiche du mois suivant et la supprime de la fiche courante. Si la fiche du mois suivant n’existe pas, le système génère une nouvelle fiche pour le visiteur en cours de traitement et pour le mois suivant. Cette nouvelle fiche a des valeurs à 0 pour les frais forfaitisés et est dans l’état « Créée ». Retour au 9
  - 8.b : le texte ainsi complété dépasse la taille maximale du champ « libelle » : le texte est tronqué par la fin au nombre de caractères du champ « libelle »

- Contraintes : néant

- Questions ouvertes : néant

### Cas d'utilisation 5

- Nom cas d’utilisation : Suivre le paiement fiche de frais
- Acteur déclencheur : Comptable
- Pré conditions : Utilisateur Comptable authentifié
- Post conditions : Néant

- Scénario nominal :

1. L’utilisateur demande à suivre le paiement des fiches de frais.
2. Le système propose de choisir une fiche de frais parmi celles à valider et mises en paiement
3. L’utilisateur sélectionne les informations et valide
4. Le système affiche le détail de la fiche de frais (frais forfaitisés et hors forfait)
5. L’utilisateur « Met en paiement » la fiche de frais
6. Le système modifie l’état de la fiche à « Mise en paiement » et met à jour la date de modification.

- Exceptions :

  - 4-a : Aucune fiche de frais n’existe, le système affiche « Pas de fiche de frais pour ce visiteur ce mois ». Retour au 2
  - 5.a : L’utilisateur indique que la fiche a été effectivement remboursée
  - 6.a : Le système modifie l’état de la fiche à « Remboursée » et enregistre la date de modification

- Contraintes : néant

- Questions ouvertes : néant
