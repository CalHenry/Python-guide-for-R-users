# Python, environnements virtuels et packages

> L'écosystème de Python, c'est aussi toute une infrastructure, mais contrairement à R, rien n'est géré pour toi par défaut. Environnements virtuels, gestionnaires de packages, versions de Python, ce chapitre démêle tout ça.

---

## Python binary
- Le Python installé est un ***interpréteur***. Il compile le script en bytecode (.pyc), puis la machine virtuelle de Python l'exécute.  
- On peut avoir plusieurs versions de Python installées (Python 3.9, Python3.12,...)

---

## Les environnements virtuels
> Si tu as déjà utilisé ***renv***, c'est la même idée, mais obligatoire en Python.

/// info | Environnement virtuel, qu'est-ce que c'est ?
///
L'environnement virtuel est un dossier qui contient les packages de ton projet. Il est géré par un package manager.

/// info | Package manager ?
///
C'est un logiciel qui gère pour toi les dépendances du projet. Plus particulièrement, il gère la compatibilité entre les packages d'un projet (installant les bonnes versions).  
La gestion des packages dans l'écosystème Python a longtemps été catastrophique comparé à R. Des dizaines de gestionnaires ont vu le jour, chacun corrigeant un des problèmes. Aujourd'hui, ont la chance d'avoir enfin des outils très performants et complets, ce qui fait que tu ne devrais pas trop souffrir !   
[UV](https://docs.astral.sh/uv/) est le gestionnaire pour Python qui change tout. [Pixi](https://pixi.prefix.dev/latest/) pour les utilisateurs de conda.


/// question | Pourquoi est-ce qu'on s'embête à créer des environnements virtuels ?   <br> Pourquoi est-ce que l'on n'installe pas les packages sur le Python de l'ordinateur et c'est tout ?
///

➡️ Problèmes de dépendances et besoin d'isoler les versions des packages.

**On ne peut pas avoir plusieurs versions d'une même librairie installées au même endroit.**  

Concrètement quand un package est installé, il se trouve dans un dossier 
```sh
site-packages/
├── numpy/                  ← code
├── numpy-1.24.0.dist-info/ ← metadata (version, deps, etc.)
```
Si j'installe numpy 2.0, les deux dossiers seront remplacés par la version 2.0 du package.  

Un environnement virtuel, c'est un nouveau dossier, indépendant, qui peut recevoir un autre dossier numpy.

```sh
project_a/.venv/lib/python3.12/site-packages/numpy/   ← v1.24
project_b/.venv/lib/python3.12/site-packages/numpy/   ← v2.0
```

➡️ Chaque version à un chemin différent et elles sont donc isolée.   
➡️ On résout les problèmes de dépendances, impossible autrement d'avoir deux projets qui utilisent deux versions différentes du même package

///success | Chaque projet doit avoir son environnement virtuel dédié.
///

---

## Comment ça fonctionne à l'intérieur

> Pour comprendre pourquoi on crée un environnement par projet et pas un seul global, il faut comprendre ce qui se passe réellement.

C'est principalement une histoire de chemins (Paths). Chaque version à un chemin différent.  

Si les environnements virtuels sont dans des dossiers différents, est-ce que je télécharge le même package à chaque fois (duplication des fichiers et utilisation inutile du disque) ?  
➡️ Oui avec pip et venv, non avec uv.

**pip** ne sait pas si le package est déjà installé sur la machine, alors il le réinstalle. -> Duplication d'installations (qui peut finir par peser sur le disque)

**uv** change ça :

- les packages sont installés dans un seul dossier (cache)

- au lieu de réinstaller, il relie avec un **hardlink** le dossier du cache avec le dossier de l'environnement.

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│  ~/.cache/uv/                ← global cache, one copy per version   │
│    numpy-1.24/                                                      │
│    numpy-2.0/                                                       │
│    pandas-2.1/                                                      │
│        │                                                            │
│        │  hardlinks                                                 │
│        ├──────────────────────────────────┐                         │
│        ↓                                  ↓                         │
│  project_a/venv/site-packages/      project_b/venv/site-packages/   │
│    numpy-1.24/  ← hardlink            numpy-2.0/  ← hardlink        │
│    pandas-2.1/  ← hardlink            pandas-2.1/  ← hardlink       │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Bonnes pratiques modernes

/// tip | Avoir l'environnement virtuel du projet directement dans le dossier du projet.
///
```sh
.
├── .venv
│   ├── bin
│   ├── lib
│   └── python3.12
│       └── site-packages
│
├── data
...
```

---

## Gestionnaires d'environnement et dépôts de packages
> Petit tour de l'écosystème, des anciennes et des nouvelles options.

### Pip & PyPI
PyPI est le dépôt **officiel** des packages Python.  
Pip est le gestionnaire de packages **officiel** de Python, il télécharge les packages depuis PyPI.  


### UV

UV est l'outil qui fait enfin consensus dans la communauté Python. Qu'est-ce qu'il apporte ?

-  **vitesse** (~10x plus rapide que pip)

- **compatibilité** (développé comme un remplaçant de pip)

- **tout-en-un** (gestionnaire de packages ET gestionnaire d'environnements)

UV fait ce qu'il doit faire et il le fait vite et bien. C'est un outil qui s'inscrit dans le futur de Python.


### Conda

Conda est un gestionnaire de packages et d'environnements.   
Développées pour les utilisateurs de Python, il sert en fait aux projets qui utilisent plusieurs langages en même temps.   
> On s'en sert particulièrement dans le milieu académique et en biologie/ pharmacie, car de nombreux packages spécifiques à ces domaines sont accessibles avec conda dans différents langages.  

Conda a des packages pour Python, R, Julia, C, C++...

Pour un utilisateur de Python, l'avantage principal est qu'il télécharge et gère les dépendances d'autres langages.   

> Certains packages Python sont construits par-dessus des librairies de C, C++ ou Fortran pour les performances (très courant pour les packages scientifiques. Les packages R sont d'ailleurs souvent basés sur les mêmes librairies).   
Conda assure que l'installation se fait correctement (là où pip installe juste la partie Python et ne gère pas les dépendances dans d'autres langages)


??? tip "Les différentes déclinaisons de conda"

    - **Anaconda** :  Distribution d'Anaconda (entreprise) de conda, avec de nombreux packages pré-installés (~3GB de packages d'après Wikipédia quand même !)
    - **miniconda** : version allégée de conda
    - **conda**-forge : dépôt communautaire de packages pour conda. Indépendant d'Anaconda (c'est la raison pour laquelle il existe, autrement, si Anaconda ferme et supprime son dépôt, on perd tous les packages conda et le moyen d'y accéder)
    - **miniforge** : alternative à miniconda mais utilise uniquement les packages de conda-forge (encore une fois pour l'indépendance vis-à-vis d'Anaconda)


### Pixi
Et Pixi, qu'est-ce que c'est ?

Pixi est un mélange de **conda-forge** et **UV** :

- Destiné aux utilisateurs de conda (remplace conda, 100% compatible)

- Intègre les standards modernes de développement Python (pyproject, environnement virtuel à la racine du dossier du projet...)

- Gère en même temps les packages issues de PyPI et de conda, meilleur des deux mondes entre UV et conda (peut installer des packages PyPI quand ils n'existent pas sur conda, ainsi on utilise un seul gestionnaire, là où avant, il fallait soi-même gérer les dépendances entre conda et PyPI).

- plus rapide que conda

### Recommandations

| Cas d'usage | Outil |
|-------------|-------|
| Projet 100% Python | UV |
| Projet Python + R | Pixi |
| Projet Python + packages scientifiques lourds | Pixi |


Je conseille de ne pas utiliser Pip car UV est simplement meilleur, ni Conda parce que Pixi est plus complet pour Python.

---

## Utiliser son environnement virtuel

Une fois l'environnement créé, il faut que Python utilise les packages qu'il contient 
et pas ceux installés ailleurs sur la machine. Il y a deux approches.

**La façon classique : activer l'environnement dans le terminal**
```
source .venv/bin/activate  # macOS / Linux
.venv\Scripts\activate     # Windows
```

Le nom de l'environnement apparaît alors dans le terminal `(.venv)`, 
indiquant que tous les appels à `python` ou `pip` pointent vers lui.
Pour en sortir : `deactivate`.

**La façon moderne avec uv : ne pas activer du tout**

Avec uv, tu n'as généralement pas besoin d'activer l'environnement. 
`uv run` s'en charge automatiquement :
```sh
uv run <script.py>
```

uv détecte le `.venv` du projet et l'utilise, sans que tu aies à penser à l'activation.   
C'est l'approche recommandée, moins d'états cachés, pas de risque d'oublier de désactiver.

Avec pixi, c'est la même logique : `pixi run` ou `pixi shell` pour une session interactive.

??? warning "`python` ou `python3` ?"

    Python 2 est mort en 2020, remplacé par Python 3.
    ```sh
    python --version   # peut retourner Python 2.x
    python3 --version  # retourne Python 3.x
    ```
    
    En pratique avec uv ou pixi, ce problème disparaît : ces outils gèrent eux-mêmes 
    quelle version de Python est utilisée dans chaque projet, indépendamment 
    de ce qui est installé sur ta machine. C'est une raison de plus de ne jamais 
    appeler Python directement depuis le terminal sans passer par ton gestionnaire.

??? tip "Quel Python tourne réellement ?"
    
    Avec plusieurs versions de Python et plusieurs environnements, il est facile de ne plus 
    savoir lequel est actif. Quelques commandes utiles :
    ```sh
    which python          # chemin de l'interpréteur actif (macOS/Linux)
    where python          # windows
    python --version      # version active
    
    uv python list        # toutes les versions Python connues de uv
    ```
    
    La règle simple : si tu passes par `uv run` ou `pixi run`, tu n'as pas à vérifier, 
    le bon Python est utilisé automatiquement. Le doute survient surtout quand on 
    appelle `python` directement dans un terminal sans être sûr de l'environnement actif.


### Fichiers important dans un projet Python

#### pyproject.toml

L'équivalent du `DESCRIPTION` quand tu fais un package R, mais utilisé pour tout projet Python. Il déclare ton projet et ses dépendances et remplace les anciens `setup.py` et `requirements.txt`.

??? abstract "Exemple minimaliste de pyproject.toml"

    [pyproject.toml](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/) est un standard **officiel** de l'écosystème Python.
    
    ```toml
    [project]
    name = "mon-projet"
    version = "0.1.0"
    description = "Une courte description"
    readme = "README.md"
    requires-python = ">=3.10"
    dependencies = [
        "numpy>=1.24",
        "pandas>=2.0",
    ]
    ```

#### Lockfile
Si tu utilise UV ou Pixi, tu va trouver un [Lockfile](https://docs.astral.sh/uv/concepts/projects/layout/#the-lockfile) (*uv.lock* ou *pixi.lock*) dans ton dossier (même concept que *renv.lock*).

Ce fichier rend le projet **reproductible**. C'est à partir de lui que l'on sait quelles versions de quels packages installer, et ce selon la configuration (OS, version de Python).   
C'est un **snapshot** des dépendances du projet.
Le lockfile est géré par le UV ou Pixi et on ne doit pas le modifier directement.

### Modules

Les modules Python sont des extensions intégrées au langage, constituant la *bibliothèque standard*. Contrairement aux bibliothèques externes, qui doivent être installées, ces modules sont déjà inclus avec Python. Pour les utiliser, il suffit de les importer dans ton code.

Voici des modules que va obligatoirement utiliser :
```python
import os             # <- interagir avec le système d'exploitation
import json           # <- lire et écrire des fichiers json
import datetime       # <- toutes les variables et fonctions temporelles
import subprocess     # <- run des commandes shell depuis Python
import re             # <- regex module
import random         # <- pseudo-random number generator
import pathlib        # <- configurer les Paths
...
```

Tu peux retrouver la liste complète dans la [documentation officielle](https://docs.python.org/3/library/index.html).
