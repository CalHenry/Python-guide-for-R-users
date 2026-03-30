# Notebooks

Pourquoi une autre librairie de notebooks alors que Jupyter existe, et qu'il sert autant pour R que Python ?

Les avantages de marimos viennent de :
  - Moderne : réactivité, intégration avec d'autres outils.
  - Uniquement pour Python et le notebook est un script python (fichier .py)
  - La philosophie
  - Fonctionnalités pratiques pour les débutants
  
Le détails des points fort et ce que ça change venant de Jupyter:

### Moderne:
- Réactivité : Quand on change la valeur d'une variable dans une cellule, toutes les cellules qui dépendent de cette valeur son automatiquement actualisée.
- Elements intéractifs : Comprendre un panel d'éléments intégratifs qui marchent directement avaec la ractivité du notebook. Par example un slider pour chosir une valeur, changer les bornes de l'axe d'un graphique...

### Uniquement Python
Le notebook marimo n'est pas un format à part comme jupyter (.ipynb) mais un simple script python .py.  

Cela donne 3 avantages majeurs: 
- Git fonctionne. Jupyter produit un fichier JSON, qui n'est pas idéal pour correctement voir les différences entre 2 versions du fichier.
- Pas besoin conversion entre notebook et script. Le notebook peut être run comme un simple script python. Si run directement, toute la partie visuelle et intéractive du notebook est ignorée et garde uniquement les actions python. Par example, si le notebook explore et nettoie un dataset avec des plots et retourne un csv dans le dossier `data`. Alors run le notebook comme un script va process les données et retourner le csv comme l'aurais fais une version script du notebook.
- Intégration avec Python. Comme le notebook est juste un script Python, on peut définir des fonctions, des classes, et les importer dans d'autres scripts python/ notebooks.

### Philosophie
Pour avoir la réactivité du notebook, on doit respecter certaines règles qui ne sont pas présente dans Jupyter:
- variables uniques : Chaque variables est unique dans le notebook. Si je créer `a = 2` dans la première cellule, alors je ne peux écrire `a = 4` dans la deuxième. Dans Jupyter c'est autorisé.  
Cela peut paraitre contraignant au premier abord "forcé de constament inventer des nouveaux nom pour tester des nouveaux code (aa= 4 puis aaa=5). Mais en réalité il y a des vrais bénéfices pour la stabilité et la robustesse du script.
Exemple: Dans jupyter, je déclare la valeur de "a" dans 2 cellules différentes (examples, a est une valeur test d'un paramètres, j'utilise le placeholder "a" dans 2 sections différentes du notebook.). La valeur de a est celle de la dernière cellule exécutées contenant "a". Si c'est celle que je veux tant mieux, si c'est l'autre, le code tourne quand même.
Il en va de même pour les x version de "df" que l'on utilise parfois. Sans plus savoir qu'est-ce que contien "df" à ce stade du notebook quand on y retourne 2 jours plus tard. Avec marimo, tu remontes là où df est définit est tu peux lire le code car il n'y a qu'un code qui le définit.

## Marimo pour les débutants

- Gestionnaire d'environnement virtuel
Marimo découvre les packages installé selon l'environnement virtuel avec lequel le notebook est lancé. Si je run un code qui demande un package que je n'ai pas installé, je reçois un pop-up qui me propose de l'installer.

En plus des différentes sections de l'éditeur, cela fait de marimo un outil agréable.
