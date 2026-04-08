# Terminal

> Ce chapitre n'est pas le plus fun du guide mais c'est un prérequis pour tous les autres : le terminal est le socle commun de tout l'écosystème, celui que R t'a toujours épargné. 

---

## Le coeur du système

Le terminal est un logiciel pour interagir directement avec le shell, l'ordinateur.  
Pas d'interface, juste des lignes de commandes.

Inhospitalier au début, il faut le voir comme un outil, très versatile qui permet d'effectuer des actions précises et simplement (c'est toujours au même endroit et toujours avec des commandes).  
De nombreux outils sont accessibles uniquement via une CLI (command line interface), ou propose une CLI en plus d'une application. Toujours dans le but d'interagir directement avec le logiciel sans avoir à passer par les interfaces.

??? info "La philosophie du terminal"

    Le terminal est l'un des piliers de l'informatique. Il est né à une époque où le clavier était le seul outil de saisie, pas de souris, pas de couleurs, pas d'interface graphique. Cette contrainte originelle a forgé une philosophie toujours aussi pertinente aujourd'hui.
    
    Tout y est frontal : un seul écran, une seule ligne d'attention, aucune profondeur à explorer. Pas de menus imbriqués, pas de boutons à chercher, une commande, un résultat.  
    Cette radicalité n'est pas un manque, c'est un choix de puissance fait par de nombreux développeurs. Taper du texte est bien plus rapide que déplacer un curseur. Une commande bien construite accomplit en une ligne ce que l'on ferait autrement en dix clics. Et comme les mains ne quittent jamais le clavier, et on ne quitte jamais le terminal, le flux de travail ne se brise jamais.
    
    
    
    L'absence d'interface graphique a aussi un effet concret sur les performances : pas de rendu visuel à recalculer en permanence, pas de ressources gaspillées à rafraîchir des fenêtres. Le logiciel fait une chose, il la fait vite.
    
    Enfin, le terminal encourage une habitude fondamentale : écrire des scripts plutôt que de répéter les mêmes actions à la main. C'est l'automatisation dans sa forme la plus directe.
    
    Rien ne t'oblige à adhérer à cette philosophie heureusement, mais tu sais maintenant pourquoi le terminal est tant utilisé dès qu'on touche à l'informatique et pourquoi une bonne partie de ce que tu fais dans ton ordinateur peut être faite plus rapidement depuis le terminal.

Voici comment j'utilise personnellement le terminal pour tous mes projets :

- Tout part du terminal : je navigue dans le dossier de mon projet et je lance mon éditeur de code depuis le terminal.

- J'utilise git depuis le terminal

- Ma gestion des fichiers et des dossiers est dans le terminal (copier, coller, couper, créer, supprimer)

- Explorer le contenu d'un script, d'un fichier de données

- Rechercher un mot ou une séquence dans un dossier sans savoir où il se trouve (avec la  commande `grep` par exemple)

Le terminal est largement personnalisable pour avoir un look plus moderne avec des couleurs ou ajouter des commandes.
Tu peux créer tes propres commandes avec des scripts et des alias, et tu peux télécharger des nouveaux outils pour améliorer ou remplacer les commandes de bases.  


Le terminal est également l'interface principale quand on travaille dans le cloud.  
Si tu dois te connecter à une machine dans un datacenter, le seul moyen d'interagir avec et de se connecter à son terminal (et de la contrôler avec son terminal).

Savoir se débrouiller dans le terminal même un peu est donc toujours utile, et facilitera tes progrès en informatique.

/// warning | Windows et Unix – Deux écosystèmes différents
Le terminal dont je parle n'est pas le terminal par défaut de Windows.

Windows utilise `Powershell` alors que les autres OS (macOS et Linux), sont sur Unix et utilisent `Bash` par défaut.  
Les commandes que je vais présenter sont des commandes de `Bash`. Si tu veux suivre cette section du guide, tu vas devoir installer Bash. (Autrement tu peux soit l'ignorer, soit regarder les équivalents Powershell des commandes présentées).  

Maintenant, je te conseille quand même d'installer Bash, car c'est ce que tu trouveras sur toutes les machines Unix, donc toutes les machines qui ne sont pas sur Windows, mais aussi dans la grande majorité des outils modernes du développeur (Docker, Data center, cloud, serveur...).

1. Installer [**git bash**](https://git-scm.com/install/windows) (si tu as déjà **git**, ignore cette étape)

    > Git Bash embarque un environnement bash minimal pour Windows. Il ne transforme pas ta machine en Linux, mais il te donne accès aux commandes essentielles. (Git, lui, fonctionne dans n'importe quel terminal Windows, PowerShell inclus.)

2. Configurer VSCode (pareil pour Positron) : ouvre la palette de commandes avec ++ctrl+shift+p++, tape "*Terminal: Select Default Profile*" et sélectionne **Git Bash**.

Le terminal intégré de VSCode ouvrira maintenant **Bash**.

> Pour aller plus loin : **WSL**. Bien au-delà de ce guide, mais utile pour ta culture : WSL (Windows Subsystem for Linux) est grossièrement une machine virtuelle Linux dans Windows. Microsoft l'a développé par nécessité : environ 70% des développeurs travaillent pour des cibles Unix (serveurs, cloud, infrastructure…), et pour les garder sur Windows, il fallait leur offrir un environnement familier et intégré. WSL est gratuit et pour tous, il s'installe en une commande avec `wsl --install` dans Powershell.
///

---

## Commandes les plus importantes


Les commandes suivent une logique simple :

- Chaque commande a plusieurs options et/ ou arguments que tu peux lui passer.  
- Tu peux en général afficher un menu d'aide pour les commandes avec le flag '--help':  
```sh
command --help
# ou la version courte
command -h
# parfois même sans tirets
command help
```

/// note | Commandes pour manipuler les fichiers et les dossiers
///
- **pwd** : retourne le dossier dans lequel tu te trouves
- **ls** : liste les fichiers et dossiers du dossier dans lequel tu te trouves
- **cd** : change de dossier (`cd path/to/target`)
- **touch** : crée un fichier (`touch myscript.py`)
- **mkdir** : crée un dossier (`mkdir data/`)
- **mv** : déplacer ou renonmer des fichiers ou des dossiers (`mv path/to/source path/to/existing_directory`)
- **cp** : copie des fichiers ou des dossiers (`cp path/to/source path/to/target`)
- **rm** : supprime des fichiers ou des dossiers (`rm path/to/file1 path/to/file2`)


/// note | Commandes pour le développement
///
- git (cf [chapitre sur Git](git.md))
- positron (`positron .` ouvre Positron sur le dossier actuel)
- code (`code .` ouvre VSCode sur le dossier actuel)
- python

La CLI de Python sert à run les scripts, mais ton script peut devenir une CLI lui-même, avec des arguments et des options. Cela permet d'ajouter de la flexibilité sur les variables utilisées dans ton script, en les définissant comme arguments.  

??? abstract "Exemple"

    Dans ce code, on a 3 flags : *input*, *output* et *json*.  
    Depuis le terminal, on utiliserait le script avec `#!shell python <script.py> --input "un/autre/path" --output "data/processed/path" --json`.  
    Afin de choisir, sans toucher au script, les chemins contenant les inputs, le chemin où déverser les outputs, et si je veux la version JSON des fichiers.
    
    ```python
    def parse_arguments():
        parser = argparse.ArgumentParser(description="Process markdown files")
        parser.add_argument(
            "--input",
            "-i",
            type=str,
            default="data/raw/scraped_pages",
            help="Input path: directory containing either several .md files or a single .md file (default=data/raw/scraped_pages)",
        )
        parser.add_argument(
            "--output",
            "-o",
            type=str,
            default="data/processed/csv/polars_offer.csv",
            help="Output file path (default=data/processed/csv/polars_offer.csv)",
        )
        parser.add_argument(
            "--json",
            action="store_true",
            help="Also save as JSON file (replaces .csv with .json in output's path)",
        )
        
        return parser.parse_args()
    ```
