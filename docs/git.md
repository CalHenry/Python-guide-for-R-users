# Git

Git est le logiciel de versionning le plus populaire et un incontournable pour tous les projets de code :

- Ne plus jamais perdre aucune version de mes codes
- Intégration avec GitHub
- Features pour développer de manières plus robuste et mieux organisée (branches)
- Traçabilité des scripts

Git est un CLI (command line interface), on s'en sert depuis le terminal avec des commandes et des arguments.  
Mais tous les IDE modernes intègrent GIT dans l'interface, ce qui permet de l'utiliser sans devoir utiliser le terminal. Plus simple à prendre en main et à utiliser pour les commandes de base mais toujours bon de savoir se débrouiller depuis le terminal.

Commandes clés:
- **git commit**
- **git add**
- **git status**
- **git push**
- **git chekout**
- (git diff)

Plutôt que d'expliquer les commandes, voici les séquences de commandes les plus utiles :
 
<details>
<summary>Faire un commit</summary>

  ```sh
  $ ->  git status           # <- liste les fichiés modifiés et pas encore commit
  On branch main
  Your branch is up to date with 'origin/main'.
  
  Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
  modified:   docs/git.md
  modified:   docs/index.md
  modified:   docs/notebooks.md
  modified:   docs/toolkit.md
  
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

  ```sh
  $ ->  git push
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
  # Créer une branche avec "-b", change automatiquement à la branche créee
  $ -> git checkout -b newbranch
  Switched to a new branch 'newbranch'
  
 # Changer de branche
  $ -> git checkout main
  Switched to branch 'main'
  Your branch is up to date with 'origin/main'.
  ```
</details>
