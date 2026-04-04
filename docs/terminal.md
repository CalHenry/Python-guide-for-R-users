# Terminal

Le terminal est un logiciel pour intéragir directement avec le shell, l'odinateur.  
Pas d'interface, juste des lignes de commandes.

Inhospitalier au début, il faut le voir comme un outil, très versatile qui permet d'effectuer des actions précises et simplement (c'est toujours au même endroit et toujours avec des commandes).  
De nombreux outils sont accessible uniquement via une CLI (command line interface), ou propose une CLI en plus d'une application. Toujours dans le but d'intéragir directement avec le logiciel sans avoir à passer par les interfaces.

<details>
<summary>La philophie du terminal</summary>

Le terminal est l'un des piliers de l'informatique. Il est né à une époque où le clavier était le seul outil de saisie, pas de souris, pas de couleurs, pas d'interface graphique. Cette contrainte originelle a forgé une philosophie toujours aussi pertinente aujourd'hui.

Tout y est frontal : un seul écran, une seule ligne d'attention, aucune profondeur à explorer. Pas de menus imbriqués, pas de boutons à chercher, une commande, un résultat.  
Cette radicalité n'est pas un manque, c'est un choix de puissance fait par de nombreux développeurs. Taper du texte est bien plus rapide que déplacer un curseur. Une commande bien construite fait en une ligne ce que dix clics accomplissent laborieusement. Et comme les mains ne quittent jamais le clavier, et on ne quitte jamais le terminal, le flux de travail ne se brise jamais.

L'absence d'interface graphique a aussi un effet concret sur les performances : pas de rendu visuel à recalculer en permanence, pas de ressources gaspillées à rafraîchir des fenêtres. Le logiciel fait une chose, il la fait vite.

Enfin, le terminal encourage une habitude fondamentale : écrire des scripts plutôt que de répéter les mêmes actions à la main. C'est l'automatisation dans sa forme la plus directe.

Rien ne t'oblige à adhéré à cette philosophie heureusement, mais tu sais maintenant pourquoi il est tant utilisé dès qu'on touche à l'informatique et pourquoi une bonne partie de ce que tu fais dans ton ordinateur peut être faite plus rapidement depuis le terminal.
</details>

Voici comment j'utilise personnellement le terminal pour tout mes projets:
- Tout part du termial: je navigue dans le dossier de mon projet et je lance mon éditeur de code depuis le terminal.
- J'utilise git depuis le terminal
- Ma gestion des fichiers et des dossiers est dans le terminal (copier, coller, couper, créer, supprimer)
- Explorer le contenu d'un script, d'un fichier de données
- Rechercher un bout de phrase dans une dossier sans savoir où le bout se trouve 
- ...

Le terminal est largement personnalisable pour avoir un look plus moderne avec des couleurs et utiliser des meilleurs outils.  
Tu peux créer tes propres commandes avec des scripts et des alias, et tu peux télécharger des nouveaux outils pour améliorer ou remplacer les commandes de bases.  


Le terminal est également l'interface principale quand on travaille dans le cloud.  
Mais si tu dois te connecter à une machine dans un datacenter, le seul moyen d'intéragir avec et de se connecter à son terminal (et de la contrôler avec son terminal).

Savoir se débrouiller dans le terminal même qu'un peu est donc toujours utilise, et ça facilitera tes progrès en informatique.

## Commades les plus importantes

- Chaque commandes à plusieurs options et/ ou arguments que tu peux lui passer.
- Tu peux toujours afficher un menu d'aide pour les commandes avec le flag '--help':
```sh
command --help
```

### Fichiers et dossiers
- **ls** : liste les fichiers et dossiers du dossier dans lequel tu te trouve
- **cd** : change de dossier 
- **touch** : crée un ficher (touch myscript.py)
- **mkdir** : crée un dossier (mkdir data/)

### Développement
- git (voir le chapitre sur Git)
- positron (avec `positron .` ouvre l'IDE sur le dossier actuel)

### Spécifique à python/ data sciences
(uv et pixi sont présentés dans le [chapitre sur les outils](toolkit.md))
- uv
- pixi
- python
