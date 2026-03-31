# Toolkit


Le bon outil au endroit c'est mieux.

## Python

<details>
<summary><a href="https://positron.posit.co/" target="_blank">Positron (IDE)</a></summary>

Positron est un fork de VSCode par Posit pour les datasciences et rapprocher créer un outil Python familier aux développeurs R. 

En 2 mots: c'est VSCode qui se déguise en RStudio. VSCode adapté pour les datasciences.  

Les avantages majeurs par rapport à VScode sont :
- Support de R et de Python nativement
- Même layout que RStudio - même logique que RStudio
- Data explorer
- UI adaptée pour Python et R (principalement la selection du language et de l'environement virtuel)
- Support natif pour Quarto, Shiny, Air (formatter et language server pour R)

C'est donc un IDE moderne, qui corriges tous les manques de VScode pour les data sciences et l'exploration de données, dans une solution intégrée.  
Positron s'inspire beaucoup de RStudio et pour le mieux.


>Posit ne compte pas arrêter de supporter RStudio, qui reste le meilleur outil pour développer en R. Positron est une super alternative pour tout utilisateur de R qui doit se mettre à Python.

</details>
 
<details>
<summary><a href="https://docs.astral.sh/uv/pip/environments/" target="_blank">UV (gestionaire d'environement)</a></summary>

UV est présenté dans la section sur les gestionnaires d'environements.

Voici les commandes les plus utiles de UV

```sh
# Doc de la CLI
uv help 
# détail d'une commande de UV
uv help <command>  # ex : uv help init

# Initialiser un projet
uv init <nom-projet>

# Ajouter/ supprimer un package
uv add <package>
uv remove <package>

# Installer ou mettre à jour l'environement virtuel
uv sync

# Schema des dépendances du projet sous forme d'arbre
uv tree
 
# Run une commande
uv run <command> # ex : uv run marimo edit <notebook.py>

# Run un script
uv run <file.py>
```
</details>



- Pixi (gestionnaire d'environement pour conda)
- Ruff (linter and formater)
<details>
<summary><a href="https://positron.posit.co/" target="_blank">Ruff (linter and formater)</a></summary>
- Pyrefly (type checker)

## Librairies Python pour aider la transition depuis R
Datasets :
    - [Polars](https://pola.rs/) - Synthax expressive proche de dyplr, chain actions. Mieux que pandas. Lazy mode comme dbplyr

<details>
<summary>Comparatif synthaxe dplyr, polars and pandas</summary>

  ```r
  # dplyr
  df %>%
    filter(mpg > 20) %>%
    select(cyl, mpg) %>%
    mutate(kpl = mpg * 0.425)
  ```  
  
  ```python
  # polars
  df.filter(pl.col("mpg") > 20) \
    .select(["cyl", "mpg"]) \
    .with_columns((pl.col("mpg") * 0.425).alias("kpl"))
  ```
  

  ```python
  # pandas
  df = df[df["mpg"] > 20][["cyl", "mpg"]]
  df["kpl"] = df["mpg"] * 0.425
  ```
</details>


Data Viz :
 - [Seaborn](https://seaborn.pydata.org/) - API moins rugeuse que Matplotlib pour les utilisateurs venant de R
 - [Plotnine](https://plotnine.org/) - ggplot2 adapté pour python (synthax similaire, pratique si on vient de R)

Notebooks :
  - [Marimo](https://marimo.io/) - Notebook pur Python, réactif et avec une philosophie intéressantes. `LINK TO NB PAGE`
    
    
    
## L'écosystème de Python pour les data sciences
- [Numpy](https://numpy.org/): implémentation pour python des vecteurs (même logique que R, tout est un vecteur (array en numpy))
- [Pandas](https://pandas.pydata.org/docs/): pour les datasets (construit par dessus numpy)
- [Scipy](https://scipy.org/) : Librairie de statistique (construit par dessus numpy)
- [scikit-learn](https://scikit-learn.org/stable/index.html) : Tout le Machine Learning, la doc, les examples. LA raison pourquoi le ML est plus populaire sur python. (construit par dessus numpy et scipy)
- [Pytorch](https://pytorch.org/) : Deep Learning, outils pour créer et déployé des réseux de neurones. Populaire dans la recherche.
- [Transformers](https://huggingface.co/docs/transformers/index) : Modèles de DL, NLP, vision, audio, video
- [Matplotlib](https://matplotlib.org/) & [Seaborn](https://seaborn.pydata.org/) : Duo pour la dataviz
- [Pydantic](https://docs.pydantic.dev/latest/) : Data validation
- [Streamlit](https://streamlit.io/) : Rshiny mais pour python
- [FastAPI](https://fastapi.tiangolo.com/) : pour les API


## Terminal
- bat
- eza
- [startship](https://starship.rs/) (good looking prompt)
