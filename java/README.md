# Mise en place d’un environnement de développement Java

Afin de développer en Java il vous faut les outils appropriés :
- Le JDK (Java development Kit) comprenant les exécutables de base (compilateur, 
archiveur, créateur de javadoc…)
- Un outil d’aide à la compilation et de gestion des dépendances tel que Maven ou Gradle

Plusieurs approches sont possibles pour bénéficier de ces outils :
- Installation en local sur votre machine
- Utilisation de version portables des outils
- Utilisation d’environnement virtualisés (avec, par exemple, Docker

Ce document vous indiquera la marche à suivre pour l’installation locale et la création d’un 
projet avec Maven.

## Installation locale

**Attention** : cette solution n’est possible que si vous bénéficiez des droits administrateurs sur 
votre machine (vous allez devoir modifier des paramètres au niveau du système d’exploitation).

### JDK

Afin d’installer de nouveaux logiciels sur votre machine il vous est conseillé d’utiliser le 
gestionnaire de paquet de votre système d’exploitation (par exemple « winget » sur Windows.

Pour le JDK 21 vous pourrez, par exemple, utiliser la commande suivante (dans un 
« Powershell ») :

```sh
winget install --id=Microsoft.OpenJDK.21 -e
```

Cette commande va installer les fichiers du Jdk sur votre système, par défaut cette installation 
se fait dans :

```
C:\Program Files\Microsoft\jdk-21.0.6.7-hotspot
```
Lors de l’installation, la commande « winget » paramètre également les variables 
d’environnement du système afin de pouvoir utiliser tous ces outils.

Les variables paramétrées sont :
- **JAVA_HOME** : variable utilisée par certains scripts de compilation de Maven
- **Path** : variable pointant vers les exécutables utilisables sur le système

Si les variables ont bien été modifiée vous devrez être en capacité d’appeler le compilateur Java 
en ligne de commande et d’afficher le chemin contenu dans « JAVA_HOME » :

```sh
echo $Env:JAVA_HOME
```

Il est possible de vérifier la version du compilateur avec la commande suivante :

```
javac --version
```

### Maven

Installation
Malheureusement, l’outil Maven n’est pas encore disponible à l’installation via Winget. Il faudra 
ajuster la variable d’environnement « PATH » manuellement pour la faire pointer vers le dossier 
contenant les exécutables 

L’installation peut être faite en suivante le guide [disponible ici](https://maven.apache.org/guides/getting-started/windows-prerequisites.html).

Une fois la variable "PATH" ajustée il est possible d'afficher la version de Maven avec la commande suivante :
```sh
mvn --version
```

# Création d'un projet avec Maven

## Procédure

1. Ouvrir un terminal et se positionner dans le dossier de sons choix (qui va accueillir le dossier 
contenant le nouveau projet.
2. Utiliser la commande suivante pour créer un projet à partir d'un archétype basique :
```sh
mvn archetype:generate "-DarchetypeGroupId=com.dominikcebula.archetypes" "-DarchetypeArtifactId=java21-basic-archetype"
```

Lors de la création Maven va vous demander deux informations :
- **groupId**
- **artifactId**

Le groupId est l'identifiant du groupe à l'origine du projet.

On choisit généralement comme **groupId** le nom du **package principal** du projet. 

L'artifactId est l'identifiant du projet au sein de ce groupe. 

L'artifactId est utilisé par défaut pour construire le nom de l'artefact final (exemple : pour un `artifactId=monprojet`, le nom du fichier jar généré sera `monprojet-version.jar`).

Bien faire attention de suivre les [recommandations Maven pour le nommage](https://maven.apache.org/guides/mini/guide-naming-conventions.html).

## Information sur les archétypes

Maven se base sur des « archétypes » qui sont des modèles de projets.

Un archétype définit :
- une arborescence du projet par défaut
- un « pom.xml » comportant un ensemble de dépendances

Les archétypes les plus populaires sont :
- maven-archetype-quickstart ;
- maven-archetype- site
- maven-archetype-webapp ;
- maven-archetype-j2ee-simple ;
- jpa-maven-archetype ;
- spring-mvc-quickstart .

Dans cette procédure il est proposé d’utiliser l’archétype de Dominik Cebual qui permet d'obtenir un projet minimaliste basé sur Java 21.

Pour plus de détails sur l’archétype utilisé veuillez vous référer au dépôt Git officiel : [https://github.com/dominikcebula/java21-basic-archetype](https://github.com/dominikcebula/java21-basic-archetype).
