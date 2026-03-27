# Python, environement virtuels et packages


## Python binary
- Le Python installé est un ***interpréteur***. Lors de l'éxécution c'est lui qui lit le code et le traduit en language machine.
- On peut (et on a souvent) plusieurs versions de python installées (Python 3.9, Python3.12...)


## Les environements virtuels

Pourquoi est-ce qu'on s'embête à créer des environements virtuels ?  
Pourquoi est-ce qu'on installes pas les packages sur le python de l'ordinateur et c'est tout ?

-> Problèmes de dépendances et besoin d'isoler les versions des packages.

**On ne peut pas avoir plusieurs versions d'une même librairie installées au même endroit.**  

Concrètement quand un package est intallé il se trouve dans un dossier 
```sh
site-packages/
├── numpy/                  ← the importable package directory
├── numpy-1.24.0.dist-info/ ← metadata (version, deps, etc.)
```
Si j'installe numpy 2.0, le dossier 1.24 sera remplacé par la version 2.0 du package.  

Un environement virtuel c'est un nouveau dossier, indépendant, qui peut recevoir un autre dossier numpy.

```sh
project_a/venv/lib/python3.12/site-packages/numpy/   ← v1.24
project_b/venv/lib/python3.12/site-packages/numpy/   ← v2.0
```

Ainsi on isole les versions, chaque version à un chemin différent.   
Et on résoult les problèmes de dépendances, impossible autrement d'avoir 2 projets qui utilisent 2 versions différentes du même package

Chaque projet doit avoir son environement virtuel dédié.

## Comment ça fonctionne à l'intérieur

C'est principalement une histoire de chemins (Paths).  
Chaque version à un chemin différent.  

Si les environements virtuels sont des dossiers différents, est-ce que je télécharges le même package à chaque fois (duplication des fichiers et utilisation inutile du disque) ?  
-> Oui avec pip et venv, Non avec uv

pip ne sait pas si le package est déjà installé sur la machine, alors il le résintalle. -> pas opti.

uv change ça:
- les packages sont installé dans un seul dossier (cache)
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

- Avoir l'environement virtuel du projet directement dans le dossier du projet
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
