# Résumé des commandes usuelles Git

## Commandes basiques

### `git init`

Crée un dépôt vide dans le répertoire courant. Après cette commande, les commandes Git sont disponibles pour la totalité de ce répertoire. Le sous-répertoire `.git` y est créé, c'est là que Git stocke tout ce qui concerne la gestion de version pour le répertoire. Le répertoire `.git` ne doit pas être modifié directement. Cependant, il peut être supprimé si vous souhaitez renoncer complètement à la gestion de ce répertoire par Git.

_Sous VS Code : équivalent au bouton "Initialize Repository"._

### `git clone <depot.git>`

Clone sur la machine locale le dépôt localisé à l'adresse spécifiée. En général, le dépôt cloné est sur Internet (adresse copiée depuis GitHub ou autre service), mais pas forcément.

### `git config user.name <nom>`

Configure le nom du committeur pour le dépôt courant. Souvent utilisé avec l'option `--global` pour utilisé le même nom sur tous ses dépôts.

### `git add <fichier_ou_repertoire>`

Passe en zone _staged_ (« indexé ») l'ensemble des modifications détectées sur `<fichier_ou_repertoire` depuis le dernier commit. Si aucun fichier ou répertoire n'est spécifié, _toutes_ les modifications sur le dépôt seront indexées. La zone _staged_ contient les fichiers qui seront pris en compte dans le prochain commit.

_Sous VS Code : équivalent au bouton `+` placé à droite des fichiers modifiés : cela les place dans la zone indexée._

### `git commit -m "<message de commit>"`

Commit une photographie de tous les fichiers indexés.

_Sous VS Code : équivalent du bouton `Commit` associé au message de commit dans la zone texte. Les fichiers indexés qui sont committés sont listés juste en dessous. Encore en dessous, on trouve la liste des fichiers modifiés qui ne sont pas indexés, et qui ne feront donc pas partie du commit._

### `git status`

Liste les fichiers modifiés et indexés (voir ci-dessus), ainsi que les fichiers _untracked_, c'est-à-dire non encore suivis pas Git (qui n'ont pas été `add`).

_Sous VS Code : c'est l'affichage du panneau "Source Control"._

### `git diff`

Affiche les différences entre les fichiers indexés et les fichiers modifiés.

### `git diff HEAD`

Affiche les différences entre les fichiers modifiés et le dernier commit.

### `git diff --cached`

Affiche les différences entre les fichiers indexés et le dernier commit.

### `git log`

Affiche la totalité de l'historique de commits du dépôt.

_Sous VS Code : l'extension "Git History" peut être installée pour remplir le même rôle._

### `git log --oneline`

Condense chaque commit sur une seule ligne (plus lisible).

### `git log -p`

Affiche un _diff_ complet pour chaque commit (différence au fur et à mesure des commits).

### `git log --<fichier>`

Affiche seulement les commits relatifs au fichier spécifié. Pratique pour voir l'évolution d'un fichier particulier.

## "_Undo_" avec Git

### `git revert <commit_ou_branche>`

Crée un nouveau commit qui annule les modifications faites par le commit spécifié (par son _hash_). Si une branche est spécifiée, annule le dernier commit de la branche.

_Sous VS Code : l'extension "Gitlens" propose la commande `revert`._

### `git reset`

Réinitialise l'index au dernier commit (comme si on n'avait rien mis dans l'index).

_Sous VS Code : équivalent du `-` à côté de la liste "Staged Changes"._

### `git reset <fichier>`

Enlève uniquement `fichier` de l'index.

_Sous VS Code : équivalent du `-` à côté d'un fichier indexé._

### `git reset --hard`

Réinitialise l'index et le répertoire courant au dernier commit. **Destructif ! Les modifications depuis le dernier commit seront définitivement perdues**.

_Sous VS Code : équivalent de la flêche "Discard All Changes" à côté de la liste "Changes"._

### `git reset --hard <lecommit>`

Réinitialise l'index et le répertoire courant au commit spécifié. **Destructif ! Supprime tous les changements depuis le dernier commit ET tous les commits qui ont suivi `lecommit`**.

## Réécrire l'historique

### `git commit --amend`

Refait un commit qui remplace complètement le dernier commit. Si rien de nouveau n'a été indexé, permet de simplement changer le message du dernier commit. À utiliser en général lorsque vous vous rendez compte rapidement que vous n'avez pas tout à fait committé la version que vous vouliez.

_Sous VS Code : commande "Commit Staged (Amend)"_

### `git rebase <base>`

Rebase (déplace) la branche courante vers `base` (commit, branche, ou une référence relative comme `HEAD^`). On utilise `rebase` si on veut éviter les _merge_ dans l'historique.

### `git rebase -i <base>`

Rebase la branche courante vers `base`, mais de manière interactive (ouvre un éditeur permettant d'indiquer quel commit on veut bouger, ignorer ou modifier).

## Travailler avec des branches

On crée et on travaille sur une branche pour développer une fonctionnalité ou corriger un bug, par exemple.

### `git checkout <branche_ou_commit>`

Se déplace sur la branche ou le commit spécifié. Si c'est sur un commit, on sera en « *DETACHED HEAD* ».

### `git switch <branche>`

« Nouvelle » commande permettant de se déplacer sur la branche de manière plus explicite.

### `git branch`

Liste toutes les branches du dépôt.

### `git branch <mabranche>`

Crée la branche `mabranche`. Il faut ensuite _checkout_ la branche pour travailler dessus.

### `git branch -b <mabranche>`

Crée la branche `mabranche` et la _checkout_ immédiatement.

### `git switch -c <mabranche>`

Nouvelle manière de faire la même chose (`-c` pour `create`).

### `git merge <mabranche>`

Fusionne `mabranche` avec la branche courante (il faut donc d'abord se placer sur la branche cible).

## Dépôts distants (_remote_)

Un dépôt distant est en général sur internet (ex : sur GitHub)

### `git remote add <nom> <url>`

Crée une nouvelle connexion à un dépôt distant.

### `git fetch <remote> <branche>`

Récupère (_fetch_) les données d'une branche distante spécifique, _sans la fusionner localement_. Il faudra fusionner pour appliquer les modifications. Si `branche` n'est pas spécifiée, récupère tout.

### `git pull <remote>`

Récupère les données d'une branche distante spécifique et tente de fusionner immédiatement. Si `branche` n'est pas spécifiée, récupère tout et fusionne. Cette commande regroupe donc en fait un _fetch_ et un _merge_.

### `fetch` ou `pull` ?

La commande `git pull` automatise la mise à jour des données en local mais peut entraîner des conflits si vous avez modifié beaucoup de fichiers. `git fetch` permet de garder son répertoire de travail à jour et de contrôler le moment où l'on souhaite fusionner les données.

### `git push <remote> <branche>`

« Pousse » (_push_) la branche locale vers le dépôt distant, avec tous les commits qui ont été effectués localement. Crée la branche `branche` sur le dépôt distant si elle n'existe pas.
