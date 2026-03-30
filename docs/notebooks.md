# Notebooks

Pourquoi une autre librairie de notebooks alors que Jupyter existe, et qu'il sert autant pour R que Python ?

Les avantages de marimo :
  - Uniquement Python, meilleure intégration avec le language
  - Versioning avec Git comme un script classique
  - Moderne : réactivité, intégration
  - La philosophie
  - Editeur plus complet que JupyterLab
  - Projet mature, maintenu et avec un communauté croissante
  
### Uniquement Python
Marimo n'a pas de format à part comme jupyter (.ipynb), c'est un simple script Python (.py).  

Cela donne 3 avantages majeurs: 
- Git fonctionne. Jupyter produit un fichier JSON, qui n'est pas idéal pour correctement voir les différences entre 2 versions du fichier.
- Pas besoin conversion entre notebook et script. Le notebook peut être run comme un simple script Python. Si run directement, toute la partie visuelle et intéractive du notebook est exécutée sans rendu visuel. Par example, si le notebook explore et nettoie un dataset avec des plots et retourne un fichier csv dans le dossier `data`. Alors run le notebook comme un script va process les données et retourner le fichier csv comme l'aurais fais une version script du notebook.
- Intégration avec Python. Comme le notebook est juste un script Python, on peut définir des fonctions, des classes, et les importer dans d'autres scripts Python/ notebooks.

### Moderne:
- Réactivité : Quand on change la valeur d'une variable dans une cellule, toutes les cellules qui dépendent de cette valeur sont automatiquement actualisée.
- Elements intéractifs : Comprend un panel d'éléments intégratifs qui marchent directement avec la ractivité du notebook. Par exemple un slider pour choisir une valeur, changer les bornes de l'axe d'un graphique...

### Philosophie
Pour avoir la réactivité du notebook, on doit respecter certaines règles qui ne sont pas présente dans Jupyter:
- variables uniques : Condition nescessaire pour la réactivité. Si je crée `a = 2` dans la première cellule, alors je ne peux pas écrire `a = 4` dans la deuxième. Dans Jupyter c'est autorisé.  
Cela peut paraitre contraignant au premier abord "forcé de constamment inventer des nouveaux nom pour tester de nouveaux codes (aa= 4 puis aaa=5). Mais en réalité il y a des vrais bénéfices pour la stabilité et la robustesse du script.
Exemple: Dans jupyter, je déclare la valeur de "a" dans 2 cellules différentes (examples, a est une valeur test d'un paramètres, j'utilise le placeholder "a" dans 2 sections différentes du notebook.). La valeur de a est celle de la dernière cellule exécutée contenant "a". Si c'est celle que je veux tant mieux, si c'est l'autre, le code tourne quand même.
Il en va de même pour les x version de "df" que l'on utilise parfois. Sans plus savoir ce que contien "df" à ce stade du notebook quand on y retourne 2 jours plus tard. Avec marimo, tu remontes là où df est défini est tu peux lire le code car il n'y a qu'une cellule qui le définit.

## Marimo pour les débutants

- Pop up d'installation si un package nescessaire n'est pas installé.  
- Pas besoin de se préocuper de l'environnement virtuel. Marimo a un mode "sandbox" qui lance le notebook dans un environnement isolé, parfait tester et explorer des solutions avec d'autres packages.
- Un éditeur complet, avec des features en plus de jupyter, comme la documentation des fonctions
- data explorer intégré
- gestionnaire des packages
-
