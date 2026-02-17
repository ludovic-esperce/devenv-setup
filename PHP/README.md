# Installation de PHP

Il est possible d'installer PHP en utilisant Winget et la commande suivante :

```sh
winget install PHP.PHP.8.4.2
```

Pour vérifier la bonne installation de PHP et la mise à jour correcte des variables d'environnement, utiliser la commande suivante :

```sh
php --version
```

# Mise en place de composer

## Installation

[Composer est un outil de gestion de dépendances pour PHP](https://getcomposer.org/doc/00-intro.md).

Il permet de :
- gérer les dépendances (bilbiothèques utilisées par le projet)
- faciliter la mise à jour : simplification de la mise à jour des bibliothèques.
- utiliser un **autoloader** : permet de trouver automatiquement les fichier à importer lorsque l'on souhaite utiliser une classe.

Procédure d'installation :
1. Télécharger et installer Composer
  - récupérer l'installateur sur le [site officiel](https://getcomposer.org/download/)
  - démarrer l'installateur et installer l'outil pour tous les utilisateurs

2. Modification de la variable d'environnement PATH
  - ajouter le dossier contenant les exécutables de `composer` dans le `PATH`

Il est possible de vérifier la bonne installation de l'outil avec la commande suivante :

```sh
composer --version
```

## Initialisation d'un projet

1. Création d'un nouveau projet :
- se positionner dans un dossier dans lequel sera créer le projet
- utiliser la commande d'initialisation :
```sh
compose init
```
- suivre les instructions

2. Installation de dépendances répértoriée sur [Packagist](https://packagist.org/) :
- ajouter une dépendance avec :
```sh
composer require <nom-paquet>
```

Plus d'informations disponibles sur composer sur l'article disponible [ici](https://www.dev-metal.com/composer-tutorial/).

# Procédure d'activation de xDebug

## Sous Windows

1. Suivre les instructions de cette page : [Wizard xdebug](https://xdebug.org/wizard)
2. Installer l'extension xDebug pour PHP : https://marketplace.visualstudio.com/items?itemName=xdebug.php-debug
3. Modifier le `launch.json` de VSCode avec le contenu suivant :
```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9003
        },
        {
            "name": "Launch currently open script",
            "type": "php",
            "request": "launch",
            "program": "${file}",
            "cwd": "${fileDirname}",
            "port": 0,
            "runtimeArgs": [
                "-dxdebug.start_with_request=yes"
            ],
            "env": {
                "XDEBUG_MODE": "debug,develop",
                "XDEBUG_CONFIG": "client_port=${port}"
            }
        },
        {
            "name": "Launch Built-in web server",
            "type": "php",
            "request": "launch",
            "runtimeArgs": [
                "-dxdebug.mode=debug",
                "-dxdebug.start_with_request=yes",
                "-S",
                "localhost:0",
                "-t",
                "./public"
            ],
            "program": "",
            "cwd": "${workspaceRoot}",
            "port": 9003,
            "serverReadyAction": {
                "pattern": "Development Server \\(http://localhost:([0-9]+)\\) started",
                "uriFormat": "http://localhost:%s",
                "action": "openExternally"
            }
        }
    ]
}
```
4. Utiliser l'icône de debug pour lancer le debugger avec l'option `Launch built-in web server`
