# Installation d'un environnement de développement Symfony

> [!IMPORTANT]  
> Une installation de `php` et `composer` doit être fonctionnelle avant de pouvoir installer `symfony-cli`.
>
> La procédure ci-dessous est une version condensée de l'excellent tutoriel [disponible ici](https://symfony.com/doc/current/setup.html).

## Installation de "symfony-cli"

Symfony CLI (pour "client") est une application utilisable dans un terminal permettant de créer et constuire des applications Symfony en ligne de commande.

La documentation officielle détaillant l'installation est [disponible ici](https://symfony.com/download).

Deux méthodes sont possibles pour installer `symfony-cli` :
- utilisation de [`scoop`](https://scoop.sh/) : installateur de logiciels en ligne de commande
- téléchargement des binaires de `symfony-cli` et modification du `path`

## Vérifier le fonctionnement de symfony-cli

La commande suivante vous permettra de vérifier que votre système est configuré de façon à pouvoir utiliser Symfony.

```sh
symfony check:requirements
```

## Initialisation d'un projet

### Site web

Dans un terminal, se rendre dans un dossier de travail et effectuez la commande suivante :

```sh
symfony new <nom-projet> --version="8.0.*" --webapp
```

Il est possible que `symfony-cli` renvoie l’erreur suivante :

```text
The openssl extension is required for SSL/TLS protection but is not available. If you can not enable the openssl extension, you can disable this error, at your own risk, by setting the 'disable-tls' option to true.
```

Si c’est le cas, il faut activer l’extension `openssl` dans le fichier `php.ini` de votre installation de PHP :

```
extension=openssl
```

### Web API

Dans un terminal, se rendre dans un dossier de travail et effectuez la commande suivante :

```sh
symfony new <nom-projet> --version="7.0.*"
```

## Démarrer un serveur de développement

Toujours dans un terminal :

```sh
cd projet/
symfony server:start
```

## Connexion de l'application à une base de données

Dans le fichier `.env`, contenant les variables d’environnement, configurer la connexion en décommentant la ligne qui correspond à votre driver de base de données : 

```conf
# customize this line!
DATABASE_URL="mysql://<utilisateur-bd>:<mot-de-passe>@<ip-serveur>:<port-sgbd>/<nom-bd>?serverVersion=<version-server>"
```

> [!WARNING]  
> Adapter au besoin les informations suivantes :
> - `<utilisateur-bd>` : utilisateur de la base de données
> - `<mot-de-passe>` : mot de passe de l'utilisateur de la base de données
> - `<ip-serveur>` : addresse IP du serveur de BDD (127.0.0.1 pour adresse loccale)
> - `<port-sgbd>` : port d'écoute du serveur de BDD (3306 par défaut pour MySQL)
> - `<nom-bd>` : nom de la base de données
> - `<version-server>` : version du SGBD (facultatif)