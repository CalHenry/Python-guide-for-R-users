# Git & GitHub

> Si tu as déjà survécu avec des fichiers `analyse_final_v2_VRAIMENT_FINAL.R`, Git est la solution propre à ce problème. C'est l'outil de versioning standard, incontournable dès qu'on travaille en équipe ou sur des projets sérieux.

## Pourquoi utiliser Git ?

- **Ne jamais perdre** une version de ton code
- **Traçabilité** : savoir qui a modifié quoi et quand
- **Travail en équipe** : merger les contributions de plusieurs personnes
- **Expérimenter sans risque** grâce aux branches

## Modèle mental

Git est comme un **photographe** qui prend des photos de ton projet à des moments précis.
```
┌─────────────────────────────────────────────────────────────────────┐
│                        3 états de GIT                               │
│                                                                     │
│   ┌──────────┐    ┌──────────┐    ┌──────────────┐                  │
│   │Working   │    │ Staging  │    │ Local Repo   │   ┌──────────┐   │
│   │Directory │───▶│  Area    │───▶│  (.git)      │──▶│ Remote   │   │
│   │(fichiers)│    │ (index)  │    │  (commits)   │   │ (GitHub) │   │
│   └──────────┘    └──────────┘    └──────────────┘   └──────────┘   │
│                                                                     │
│   Tu modifies    git add =            git commit =      git push =  │
│   tes fichiers   "préparer la         "prendre la         "envoyer  │
│   ici            photo"               photo"              la photo" │
└─────────────────────────────────────────────────────────────────────┘
```
Chaque **commit** est une photo horodatée de ton projet. Tu peux revenir à n'importe quelle photo à tout moment.


### Git ≠ GitHub
```
   GIT LOCAL                    GITHUB (Remote)
┌────────────────┐          ┌────────────────────┐
│                │  push    │                    │
│   .git/        │─────────▶│   github.com/      │
│   (ton ordi)   │  pull    │   ton-repo         │
│                │◀─────────│                    │
└────────────────┘          └────────────────────┘
Tu travailles ici              Backup & collaboration
```

Git fonctionne **seul** sur ton ordi. GitHub est juste un cloud pour sauvegarder et partager ton travail. Il apporte ensuite des fonctionnalités pour le travail en équipe et la collaboration sur un même repo.


## Git en pratique

Git est un outil en ligne de commande (CLI), mais les IDE modernes (VSCode, RStudio) l'intègrent directement.

### Commandes essentielles

| Commande | Rôle |
|----------|------|
| `git status` | Voir l'état des fichiers |
| `git add <fichier>` | Indexer un fichier |
| `git commit -m "message"` | Créer un snapshot |
| `git push`/ `git pull`| Envoyer sur GitHub/ Recevoir de GitHub|
| `git switch -c <branche>` | Créer une branche |
| `git switch <branche>` | Changer de branche |
| `git diff` | Comparer les modifications |

### Les 4 états d'un fichier
```
┌─────────────────────────────────────────────────────────────────────┐
│   ┌────────────┐                                                    │
│   │ Untracked  │  ← Nouveau fichier, ignoré par Git                 │
│   └─────┬──────┘                                                    │
│         │ git add                                                   │
│         ▼                                                           │
│   ┌────────────┐                                                    │
│   │  Staged    │  ← Prêt à être photographié                        │
│   └─────┬──────┘                                                    │
│         │ git commit                                                │
│         ▼                                                           │
│   ┌────────────┐                                                    │
│   │ Committed  │                                                    │
│   │ (dans .git)│                                                    │
│   └─────┬──────┘                                                    │
│         │ (modification)                                            │
│         ▼                                                           │
│   ┌────────────┐     git add       ┌────────────┐                   │
│   │  Modified  │──────────────────▶│  Staged    │                   │
│   └────────────┘                   └─────┬──────┘                   │
│                                          │ git commit               │
│                                          ▼                          │
│                                    ┌────────────┐                   │
│                                    │ Committed  │                   │
│                                    └────────────┘                   │
└─────────────────────────────────────────────────────────────────────┘
```

### Séquences typiques

///example | **Faire un commit**  
"Tu viens de modifier deux fichiers et tu veux sauvegarder uniquement l'un d'eux"
///

```sh
# 1. Voir ce qui a changé
$ git status
# 2. Ajouter les fichiers souhaités
$ git add docs/git.md
# 3. Créer le commit
$ git commit -m "doc: améliorer la section git"
```

---

///example | **Push to remote après un commit**  
"Tu viens de faire un commit et tu veux le push sur GitHub"
///

```sh
$ git push # sans arguments, push tous les commits de la branche actuelle à sa jumelle sur GitHub
To https://github.com/you/your_repo.git
    2c24012..2249eb5  main -> main
```

---

///example | **Lier un repo local à GitHub**  
"Tu as déjà initié git sur ton dossier et tu veux le lier à un repo GitHub que tu viens de créer sur le site.
///
```sh
# Si le repo local existe déjà 
$ git remote add origin https://github.com/user/monrepo.git
$ git branch -M main
$ git push -u origin main
```

---

///example | **Créer et/ ou changer de branche**  
"Tu veux ajouter une feature ou tester quelque chose"
///

```sh
# Créer une branche avec "-c", change automatiquement à la branche créée
$ git switch -c newbranch
Switched to a new branch 'newbranch'

# Changer de branche
$ git switch main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
```

---

///example | **Comparer 2 versions d'un fichier**  
"Tu veux savoir quels sont les changements depuis la version du dernier commit. Par exemple pour écrire le message du commit à venir"
///

```sh
# Retourne le diff pour tous les fichiers modifiés et non commit
$ git diff

# Tu peux également préciser quel fichier
$ git diff docs/git.md
```

## Concepts

**.gitignore**

Par défaut, Git suit tous les fichiers du dossier, or, on ne veut pas tracker tous les fichiers de tous les dossiers.  
Par exemple le dossier `data/`, ou les informations secrètes (comme les clefs API), ou les fichiers que l'on ne veut pas voir sur GitHub.

On utilise donc un fichier spécial **.gitignore** qui contient simplement les noms des dossiers et fichiers à ignorer pour git.

??? abstract "Exemple de .gitignore"

    ```sh
    # manually added
    .env                   # <- secrets
    data/
    models/*               # <- '*' dit à git d'ignorer tout ce que contient le dossier
    !models/*.py           # <- '!' = inverse - on n'ignore PAS les fichiers .py 
    !models/README.md      # <- on n'ignore pas le readme
    
    
    # Python-generated files
    __pycache__/
    *.py[oc]
    build/
    dist/
    wheels/
    *.egg-info
    
    # Virtual environments
    .venv
    ```


**Branches**

Les branches (comme pour un arbre) permettent d'expérimenter sans casser le code principal (main). 
On se détache de la branche principale. Il y a donc une branche active sur laquelle on fait les commits, et les autres branches. 
On peut changer de branche à tout moment et ainsi développer plusieurs parties du projet en même temps.

/// tip | Par exemple  
Tout le code se trouve dans un seul script, le projet grandit et ce n'est plus maintenable. On veut changer la structure du code.  
///
Pour garder **main** intacte (car cette version du projet est validée et fonctionne), on crée une branche. Dans cette branche, on va créer de nouveaux scripts, répartir le code, gérer les imports... On fait les commits dans la branche, on teste le code. Une fois validé, on fusionne (merge) dans main.

```
┌─────────────────────────────────────────┐
│                                         │
│  main:                                  │
│    o---o---o---o                        │
│         \                               │
│          \---o---o   feature-branch     │
│                                         │
│  ↑ main peut continuer d'avancer        │
│  ↳ dev en parallèle sur feature-branch  │
│                                         │
└─────────────────────────────────────────┘
```
Les branches sont l’une des fonctionnalités les plus puissantes de Git. Elles permettent de travailler sur plusieurs parties d’un projet en parallèle, ou même de maintenir différentes versions du même projet sans interférer les unes avec les autres.  

En pratique, quand tu changes de branche, Git met automatiquement à jour les fichiers que tu vois. Un même fichier peut exister en plusieurs versions selon les branches. Git sait toujours quelle version appartient à quelle branche.


## Bonnes pratiques

- **Faire des commits atomiques** : un commit = une seule modification logique. (Il vaut mieux beaucoup de commits simples qu'un commit avec 15 modifications réparties sur quatres fichiers)

- **Écrire des messages de commit explicites** : `"fix: corriger bug sur login"` plutôt que `"modif"`. (Tu peux t'aider de mots clefs qui orientent directement le thème du commit "fix:", "feat", file:"... )

??? note "Exemple de messages de commits pour data scientists"
    
    Les messages de commits sont comme la documentation dans le code, ça peut paraitre évident, mais le toi dans 2 mois qui va devoir comprendre où tu as fait telle modif et surtout pourquoi, va te remercier. Lire un message de commit est bien plus rapide que de devoir se plonger dans le code.
    
    ```
    fix & file:
    
    fix:
    - update how Paths are written in config.py -> updates in the scripts
    that uses them
    - update the dataframe schema in build_dataset.py
    file:
    - merge.py can be run to merge the 2 datasets created by
    build_dataset.py and pipeline.py
    ```
    
    ```
    feat & fix
    
    fix: type checker complaints about Vector() of lancedb, fixed with Annotated
    feat: add doc_id as a parameter so the user can choose the document in
    the agent run function. doc_id is added to RAGDeps
    ```
    
    ```    
    refactor:
    
    new folder structure:
    - entry points in ./scripts/
    - ingestion pipeline in src/rag/ingestion/
    - query pipeline in src/rag/query
    ```

- **push régulièrement** : Si c'est sur GitHub c'est en sécurité.

- **commit tant que c'est frais** pour éviter d'oublier les raisons des changements
