# Python, environement virtuels et packages


## Python binary
- Le Python installé est un ***interpréteur***. Lors de l'éxécution c'est lui qui lit le code et le traduit en language machine pour qu'il soit exécuté.
- On peut (et on a souvent) plusieurs versions de python installées (Python 3.9, Python3.12,...)


## Les environements virtuels

Qu'est-ce que c'est ?
> Logiciel qui gère pour nous les dépendances du projet. Plus particulièrement, il gère pour nous la compatibilité entre les packages d'un projet (installant les bonnes versions).  
La gestion des packages dans l'écosystème python a toujours été catastrophique comparé à R. Des dizaines de gestionaires on vu le jour, chacun corrigeant un des problèmes. Aujourd'hui on la chance d'avoir enfin des outils très performant et enfin complet, ce qui fait que tu ne devrais pas trop souffrir !   
UV est le gestionaire pour Python qui change tout. Pixi pour les utilisateurs de conda.


Pourquoi est-ce qu'on s'embête à créer des environements virtuels ?  
Pourquoi est-ce qu'on installes pas les packages sur le python de l'ordinateur et c'est tout ?

-> Problèmes de dépendances et besoin d'isoler les versions des packages.

**On ne peut pas avoir plusieurs versions d'une même librairie installées au même endroit.**  

Concrètement quand un package est intallé il se trouve dans un dossier 
```sh
site-packages/
├── numpy/                  ← code
├── numpy-1.24.0.dist-info/ ← metadata (version, deps, etc.)
```
Si j'installe numpy 2.0, les deux dossiers seront remplacés par la version 2.0 du package.  

Un environement virtuel c'est un nouveau dossier, indépendant, qui peut recevoir un autre dossier numpy.

```sh
project_a/.venv/lib/python3.12/site-packages/numpy/   ← v1.24
project_b/.venv/lib/python3.12/site-packages/numpy/   ← v2.0
```

-> Chaque version à un chemin différent et elles sont donc isolée.   
-> On résoult les problèmes de dépendances, impossible autrement d'avoir 2 projets qui utilisent 2 versions différentes du même package

Chaque projet doit avoir son environement virtuel dédié.

## Comment ça fonctionne à l'intérieur

C'est principalement une histoire de chemins (Paths).  
Chaque version à un chemin différent.  

Si les environements virtuels sont des dossiers différents, est-ce que je télécharges le même package à chaque fois (duplication des fichiers et utilisation inutile du disque) ?  
-> Oui avec pip et venv, Non avec uv.

pip ne sait pas si le package est déjà installé sur la machine, alors il le résintalle. -> pas opti.

uv change ça:
- les packages sont installés dans un seul dossier (cache)
- au lieu de réinstaller, on utilise un chemin qui pointe vers la version voulue.
```sh
~/.cache/uv/                        ← global cache, one copy per version
  numpy-1.24/
  numpy-2.0/
  pandas-2.1/
       │
       │  hardlinks
       ├──────────────────────────────────┐
       ↓                                  ↓
project_a/venv/site-packages/      project_b/venv/site-packages/
  numpy-1.24/  ← hardlink            numpy-2.0/  ← hardlink
  pandas-2.1/  ← hardlink            pandas-2.1/  ← hardlink
```


## Les bonnes pratiques modernes

- Avoir l'environement virtuel du projet directement dans le dossier du projet.
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

## Pip & PyPi
PIP est le gestionnaire de packages **officiel** de Python, il télécharge les packages depuis PyPi.

Pypi est le dépôt **officiel** des packages python.


## UV

UV c'est l'outil qui fait enfin concensus dans la communauté Python. Ce qu'il apporte ?
-  **vitesse** (~10x plus rapide)
- compatibilité (développé comme un remplaçant de pip, donc 100% compatible)
- tout en un (gestionnaire de packages ET gestionnaire d'environements)

## Conda

Conda est un gestionaire de packages et d'environements. A la base pour les utilisateurs de Python, il sert en fait au projets qui utilisent plusieurs languages en même temps. 
On s'en sert particulièrement dans le milieu académique et en biologie car de nombreux packages spécifiques à ces milieux sont accessiblent avec conda pour différents languages.

Conda c'est aussi un dépôt de packages (python, R, julia, C, C++).  
- Pour un utilisateur de python : télécharge et gère les dépendances d'autres languages. Nombreux sont les packages python qui sont construit par dessus des packages écrit en C, C++ ou Fortran pour les performance (très courant pour les packages scientifiques. Les packages R sont d'ailleurs souvent basé sur les mêmes librairies). Conda assure que l'installation se fait correctement (là ou pip installe juste la partie python et ne gère pas les dépendances dans d'autres languages)


<details>
<summary>Les différentes déclinaisons de conda</summary>

- Anaconda :  Distribution d'Anaconda (entreprise) de conda, avec de nombreux packages pré-installés (~3GB de packages d'après wikipédia quand même !)
- miniconda : version allégée de conda
- conda-forge : dépôt communaitaire de packages pour conda. Indépendant de Anaconda (c'est la raison pour laquelle il existe, autrement, si Anaconda ferme et supprime sont dépôt on perd tous les packages conda et le moyen d'y accéder)
- miniforge : alternative à miniconda mais utilise uniquement les packages de conda-forge (encore une fois pour l'indépendance d'Anaconda)
</details>

## Pixi
Et Pixi, c'est qui ?

Pixi c'est le mélange de conda-forge et UV :
- Destiné aux utilisateurs de conda (remplace conda, 100% compatible)
- Intègre les standards de développement Python (pyproject, environement virtuel à la base du dossier du projet, ...)
- Gère en même temps les packages issues de PyPi et de conda, meilleur des 2 mondes entre UV et conda (peut installer des packages PyPi à travers UV, si la version conda n'existe pas et toujours utilisé un seul gestionnaire, là où avant il fallait sois-même gérer les dépendances entre les 2 mondes).
- plus rapide que conda (algorithme de résoulution des dépendances plus rapide)
