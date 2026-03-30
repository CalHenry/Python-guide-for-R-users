# Toolkits


Le bon outil au endroit c'est mieux.

## Python

- Positron (IDE)
- UV (gestionaire d'environement)
- Pixi (gestionnaire d'environement pour conda)
- Ruff (linter and formater)
- Pyrefly (type checker)

### Librairies Python pour aider la transition depuis R
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
 - [seaborn](https://seaborn.pydata.org/) - API moins rugeuse que Matplotlib pour les utilisateurs venant de R

Notebooks :
  - [marimo](https://marimo.io/) - Notebook pur Python, réactif et avec une philosophie intéressantes. `LINK TO NB PAGE`
    
    
    
### L'écosystème de Python pour les data sciences
- numpy: implémentation pour python des vecteurs (même logique que R, tout est un vecteur (array en numpy))
- pandas: pour les datasets (construit par dessus numpy)
- [Scipy](https://scipy.org/) : Librairie de statistique (construit par dessus numpy)
- scikit-learn : Tout le Machine Learning, la doc, les examples. LA raison pourquoi le ML est plus populaire sur python. (construit par dessus numpy et scipy)
- Pytorch : Deep Learning, outils pour créer et déployé des réseux de neurones. Populaire dans la recherche.
- Transformers : Modèles de DL, NLP, vision, audio, video
- matplotlib & seaborn : Duo pour la dataviz
- Pydantic : Data validation
- Streamlit : Rshiny mais pour python
- FastAPI : pour les API


## Terminal
- bat
- eza
- [startship](https://starship.rs/) (good looking prompt)
