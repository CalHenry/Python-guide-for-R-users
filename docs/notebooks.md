# Notebooks

Pourquoi une autre librairie de notebooks alors que Jupyter existe, et qu'il sert autant pour R que Python ?

<details>
<summary>Critiques de Jupyter</summary>

- État caché et ordre d'exécution
Les cellules Jupyter peuvent être exécutées dans n'importe quel ordre, ce qui crée un problème subtil :
```python
# Cell 1
a = 10
# Cell 2
b = a * 2
print(b)  # affiche 20
```

Si je modifie `a = 5` dans la cellule 1 sans ré-exécuter la cellule 2, le notebook affiche toujours `b = 20`, une valeur qui ne correspond plus au code visible. C'est le **hidden state** : l'état réel du kernel diverge silencieusement de ce qu'on lit.  

Concrètement, ça mène à un pattern fréquent : les premières cellules tournent bien, on modifie des valeurs au fil de l'exploration, et à un moment le notebook retourne une erreur ou un résultat inattendu, sans qu'on sache exactement quelle combinaison de cellules avait produit le bon résultat.

- Reproductibilité :  
C'est la conséquence directe de l'état caché : relancer le même notebook du début à la fin peut produire des résultats différents de ceux affichés, voire planter. Ça demande une discipline constante pour s'assurer que les cellules sont dans le bon ordre et que les variables sont dans l'état attendu.

- Git diff illisible :  
Le format `.ipynb` mélange code et outputs sérialisés en JSON, ce qui rend les diffs quasiment inexploitables pour une revue de code.

Ces limitations sont peu gênantes pour de l'exploration rapide ou des notebooks courts, et c'est là que Jupyter excelle vraiment. C'est un outil pédagogique excellent, très accessible pour les débutants, et qui supporte R et Python.  
Mais dès que le code se complexifie, se rallonge ou s'inscrit dans un contexte de production, ces problèmes deviennent pesants.

- Pour R, Quarto adresse une partie de ces problèmes.
- Pour Python, Marimo est une alternative moderne conçue explicitement pour les éviter et c'est ce que nous allons voir dans la suite de ce chapitre.

</details>

Les avantages de marimo :
  - Moderne : réactivité, intégration
  - Uniquement Python, meilleure intégration avec le language
  - Versioning avec Git comme un script classique
  - La philosophie
  - Editeur complet
  - Projet mature, maintenu et avec un communauté croissante
  
### Uniquement Python
Marimo n'a pas de format à part comme jupyter (.ipynb), c'est un simple script Python (.py).  

Cela donne 3 avantages majeurs: 
- Git fonctionne. Jupyter produit un fichier JSON, qui n'est pas idéal pour correctement voir les différences entre 2 versions du fichier.
- Pas besoin conversion entre notebook et script. Le notebook peut être run comme un simple script Python. Si run directement, toute la partie visuelle et intéractive du notebook est exécutée sans rendu visuel. Par example, si le notebook explore et nettoie un dataset avec des plots et retourne un fichier csv dans le dossier `data`. Alors run le notebook comme un script va process les données et retourner le fichier csv comme l'aurais fais une version script du notebook.
- Intégration avec Python. Comme le notebook est juste un script Python, on peut définir des fonctions, des classes, et les importer dans d'autres scripts Python/ notebooks.

### Moderne:
- Réactivité : Quand on change la valeur d'une variable dans une cellule, toutes les cellules qui dépendent de cette valeur sont automatiquement actualisée.
- Elements interactifs : Comprend un panel d'éléments intégratifs qui marchent directement avec la ractivité du notebook. Par exemple un slider pour choisir une valeur, changer les bornes de l'axe d'un graphique...

### Philosophie
Pour avoir la réactivité du notebook, il doit respecter certaines règles qui ne sont pas présente dans Jupyter:
- variables uniques : Condition nescessaire pour la réactivité. Si je crée `a = 2` dans la première cellule, alors je ne peux pas écrire `a = 4` dans la deuxième.  
Cela peut paraitre contraignant au premier abord "forcé de constamment inventer des nouveaux nom pour tester de nouveaux codes (aa= 4 puis aaa=5). Mais en réalité il y a des vrais bénéfices pour la stabilité et la robustesse du script.  

<details>
<summary>Exemple</summary>

Reprennons l'exemple du début du chapitre :

```python
# Cell 1
a = 10
# Cell 2
b = a * 2
print(b)  # affiche 20
```
Si je change pour `a=5`, la cellule 2 va automatiquement s'actualiser avec la nouvelle valeur `b=10`. (Tu peux désactiver la réactivité automatique, dans ce cas la cellule 2 gagne une bordure rouge qui indique qu'elle n'est pas à jour avec le reste du notebook.)

</details>


## Fonctionnalités de Marimo

Marimo, comme JupyterLab, contient un environnement complet avec différents panels et intégrations, qui rendent son utilisation simple et intuitive.  
Je ne présente pas tout ici, je te laisse découvrir le reste.

- **Package manager intégré**, qui te laisse installer des packages sans passer par le terminal, et qui affiche un pop up si tu essaye de run une cellule avec un package qui n'est pas installé dans l'environnement virtuel. Marimo fonctionne très bien avec UV et Pixi.
 - **Mode "sandbox"** : environnement isolé à la volée, enlève le besoin de se préocuper de l'environnement virtuel du projet. 
- **Data explorer** : Widget interactifs pour les dataframes, explorateur de rows et de colonnes avec des graphiques des distributions, et un constructeur de graphique no-code. Tout pour rapidement manipuler et explorer les données, sans devoir écrire du code pour interagir avec les données. (Quand je découvre des nouvelles données je passe toujours par là)
![marimo_data_explorer](screenshots/marimo.png)

- **Documentation** : Clique sur une fonction et affiche sa documentation dans un panel.
- **Scratchpad** : C'est comme une cellule indépendante du notebook, tu peux tester tes codes, utiliser les mêmes noms de variable que dans le notebook sans que marimo retourne une erreur. 

Marimo inclut aussi une sections spéciale pour les secrets, un terminal intégré et supporte le formatting avec Ruff.  

L'ensemble rend le travail de données à la fois plus agréable et plus puissant qu'avec un IDE classique.
