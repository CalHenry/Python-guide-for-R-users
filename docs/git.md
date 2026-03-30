# Git & GitHub

Git (local) est le logiciel de version control le plus populaire et un incontournable pour tous les projets de code.  
GitHub (remote) est une plateforme de Microsoft qui hébeberge les "repositories" git.  


- Ne plus jamais perdre aucune version de mes codes
- Intégration avec GitHub
- Outil pour développer de manière plus robuste et mieux organisée (branches)
- Traçabilité des changements

Il est important de comprendre la relation entre Git et GitHub.  
Ils sont voué à être des miroirs, l'un en local et avec qui ont travaille activement, l'autre un dépôt, sur une plateforme dédiée à la collaboration.  
Quand on travaille seul on exploite peut les fonctionnalités de GitHub, mais en équipe, la plateforme prend tout son sens.  
Rien n'oblige à utiliser GitHub, c'est Git qui est le plus important, mais tout avoir sur GitHub, c'est la sécurité de ne jamais perdre son travail, c'et pouvoir le partager ou le télécharger sur n'importe quel ordinateur connecté à internet.

## Git 
Git est un CLI (command line interface), on s'en sert depuis le terminal avec des commandes et des arguments.  
On aussi s'en servir avec les IDE modernes qiu intègrent GIT dans l'interface, ce qui permet de gérer Git sans devoir utiliser le terminal. Plus simple à prendre en main et à utiliser pour les commandes de base mais c'est toujours bon de savoir se débrouiller depuis le terminal.

Commandes clés:
- **git commit**
- **git add**
- **git status**
- **git push**
- **git switch**
- **git diff**

## Concepts
Git fonctionne en indexant les fichiers et les changements. Il conserve chaque version d'un fichier depuis sa première apparition dans un commit.
De base Git propose de suivre tous les fichiers d'un répo, or on veut en ignorer certains. On utilise don un fichier spécial **.gitignore** et on inscrit tous les fichiers ou dossier à ne pas traquer avec Git. Par example le dossier `data/`.

Un fichier peut être dans 4 étas pour Git:
- Untrack : Ignoré ou nouveau
- Track : Suivi, connu
- Stage : Prêt, indexé
- Unstaged : Modifié, non-indexé

Stage est une étape obligatoire pour un fichier. C'est là que Git indexe les changements.

Plutôt que d'expliquer les commandes, voici les séquences de commandes les plus utiles :

<details>
<summary>Faire un commit</summary>

"Tu viens de modifier deux fichiers et tu veux sauvegarder uniquement l'un d'eux"

1. `git add <file>` : sélectionner les fichiers à inclure dans le prochain commit.
2. commit les fichiers indexés

  ```sh
  $ ->  git status           # <- liste les fichiers modifiés et pas encore commit
  On branch main
  Your branch is up to date with 'origin/main'.
  
  Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
  modified:   docs/git.md
  modified:   docs/notebooks.md
  
  Untracked files:
  (use "git add <file>..." to include in what will be committed)
  mindmap.md
  
  no changes added to commit (use "git add" and/or "git commit -a")
  
  $ -> git add docs/git.md
  
  $ -> git commit -m "doc: add 'command sequence' section"
  [main 2249eb5] add doc: add 'command sequence' section
   1 file changed, 29 insertions(+), 2 deletions(-)
  ```
</details>

<details>
<summary>Push to remote après un commit</summary>

"Tu viens de faire un commit et tu veux le 'push' sur GitHub"

  ```sh
  $ ->  git push # sans arguments, push tous les commits manquant à Github
  To https://github.com/CalHenry/MBook.git
     2c24012..2249eb5  main -> main
  ```
</details>

<details>
<summary>Commande pour lier un repo github (origin) avec le git du projet (main)</summary>

  ```sh
  # when the local git already exist
  $ -> git remote add origin https://github.com/CalHenry/MBook.git
  $ -> git branch -M main
  $ -> git push -u origin main
  ```
</details>

<details>
<summary>Créer et/ ou changer de branche</summary>

  ```sh
  # Créer une branche avec "-c", change automatiquement à la branche créee
  $ -> git switch -c newbranch
  Switched to a new branch 'newbranch'
  
 # Changer de branche
  $ -> git switch main
  Switched to branch 'main'
  Your branch is up to date with 'origin/main'.
  ```
</details>

<details>
<summary>Comparer 2 versions d'un fichier</summary>

  ```sh
  $ -> git diff 
  Switched to a new branch 'newbranch'
  
 # Changer de branche
  $ -> git switch main
  Switched to branch 'main'
  Your branch is up to date with 'origin/main'.
  ```
</details>


## Bonnes pratiques
