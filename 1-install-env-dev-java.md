# Mise en place d'un environnement de développement Java

## Introduction

L'objectif de cette journée est de mettre en place un environnement de développement Java qui permette:

 - le développement d'applications *standalone* et leur déploiement
 - le développement d'applications Web et leur déploiement

Notre objectif est de nous doter d'un outil de travail nous permettant de créer des applications Java ou Java EE.

### Déroulement de la session

A partir des choix proposés, vous allez installer par vous même les différents outils et les configurer.

L'objectif, pour chacun des outils, est d'être capable de tester son utilisation (par exemple en réussissant le lancement d'un programme Hello World).

L'objectif est également que vous soyez curieux: posez des questions, émettez des hypothèses.

### Choix des technologies

Les technologies proposées ici sont couramment utilisées dans le monde du développement Java. Cependant, le choix qui a été fait ici ne fait pas office de recommandation ni d'obligation. A vous d'être critique et d'adapter votre outil de travail en fonction de vos habitudes et de vos préférences.

L'IDE choisie est **Eclipse**.

Le serveur d'application Web est **Tomcat**.

L'outil de build (build tool) est Gradle**.

L'outil de tests unitaires est JUnit.

## Installation

### Eclipse

Installer Eclipse pour développeur Java EE (fichier `eclipse-jee-oxygen-1a*`) sur votre machine.

#### Application Java

Créer un projet pour une application Java (Java Project). Créer un programme Hello World dans le paquet `com.example.hello`. Exporter un JAR exécutable pour ce programme.

Exécuter ce JAR.

#### Application Web

Vous allez suivre la procédure décrite ici: http://www.srccodes.com/p/article/2/JSP-Hello-World-Program-using-Eclipse-IDE-and-Tomcat-web-server

L'absence de serveur Tomcat configuré va empêcher votre projet de compiler. Il faut donc installer Tomcat sur votre machine.

Nous allons choisir la version 7.x de Tomcat.

Regardez cette page pour des instructions sur l'[installation de Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/setup.html)

La procédure à suivre pour MacOS est [ici](https://wolfpaulus.com/mac/tomcat/)

Une fois cela fait, regardez [cette page](https://stackoverflow.com/questions/4076601/how-do-i-import-the-javax-servlet-api-in-my-eclipse-project) pour trouver comment configurer le serveur nouvellement installé dans Eclipse. Vous devrez également suivre les instructions données [ici](https://stackoverflow.com/questions/22756153/the-superclass-javax-servlet-http-httpservlet-was-not-found-on-the-java-build) pour que le projet puisse se lancer.

### Machine virtuelle de test

Nous allons maintenant déployer une machine virtuelle qui nous permettra de tester nos programmes (Web). Nous allons utiliser pour cela un système de virtualisation : VirtualBox (fichiers fournis).

Vous pourrez lancer sur ce système une machine virtuelle contenant un serveur Tomcat 7.0 préinstallé: `turnkey-tomcat-14.2-jessie-*`

Démarrez cette VM et entrez un mot de passe. Attention, le clavier est en QWERTY au moment de l'installation, mais il devra être entré par la suite avec un clavier français. À vous de déterminer comment entrer ce mot de passe correctement.



#### Déploiement d'un WAR

Un WAR est une archive contenant une application Web.

Depuis votre projet Eclipse, exportez un WAR puis déployez le dans la VM.

Une fois cela fait, déployez ce WAR dans votre serveur virtuel et testez-le.

Quel est l'intérêt d'utiliser une VM pour les tests ?

### Tests Unitaires

Vous allez maintenant créer un test unitaire avec JUnit

Pour cela, je vous propose de rajouter une classe HelloWorldTest dans le premier projet Java.

[Cette page](http://www.tutorialspoint.com/junit/junit_plug_with_eclipse.htm) donne un exemple d'utilisation de JUnit: utilisez le code ci-dessous.

```java
package com.example.hello;

import org.junit.jupiter.api.Test;

import static org.junit.Assert.assertTrue;

public class HelloWorldTest {
	@Test
	public void testHelloWorld() {
		assertTrue("Hello world", 1 == 1) ;
	}
}
```

Faites évoluez ce code pour y ajouter des tests fictifs et testez-le.

D'autres exemples peuvent être trouvés ici:

 - http://junit.org/junit5/docs/current/user-guide/
 - https://howtoprogram.xyz/java-technologies/junit-5-tutorial/
 - https://howtoprogram.xyz/2016/08/10/junit-5-vs-junit-4/
 - http://users.csc.calpoly.edu/~djanzen/tdl/tddintro/helloworld/

### git

Pour que notre environnement de travail soit complet, il faut que git soit configuré pour un travail en mode projet.

Pour tous les projets qui précèdent, mettez en place un dépôt git permettant de centraliser les informations au sein de votre équipe. Pour cela, vous devrez peut-être créer une "organisation" sur *github* (par exemple) ou sur tout autre site/serveur de votre choix.



### Gradle

Gradle est un outil de build (au fait, qu'est-ce qu'un *build tool* ?). Il est capable de s'interfacer avec Ant ou Maven (d'autres *build tools*).

#### Installation manuelle

Regardez la page suivante: https://gradle.org/install/#install

#### Installation dans Eclipse

Dans le Marketplace d'Eclipse, cherchez le terme `buildship`. Si le plugin est déjà installé, mettez-le éventuellement à jour.

#### Utilisation

Suivre les instructions données sur [cette page](https://guides.gradle.org/building-java-applications/) pour votre projet Hello World (commencez par créer un projet de type `basic`).

Ajouter au fichier `build.gradle` les éléments suivants pour [créer un JAR exécutable](https://stackoverflow.com/questions/21721119/creating-runnable-jar-with-gradle):

```build
jar {
    manifest {
        attributes 'Main-Class': 'com.example.hello.HelloWorld'
    }
}

```

Exécuter `gradle build` et vérifiez que le fichier `./build/libs/HelloWorld.jar` est créé dans votre répertoire.


#### Tests unitaires

Une question a été posée [ici](https://stackoverflow.com/questions/20707017/how-to-run-junit-tests-with-gradle) sur `stackoverflow`.

Etudiez cette question et essayez de reproduire la demande et la solution dans un projet.

Pour ce projet, il vous est proposé de tester les fonctions mathématiques suivantes:

 - `multiplier` deux nombres entiers;
 - `additionner` deux nombres entiers;
 - `soustraire` deux nombres entiers.

Quel peut être l'intérêt d'un tel outil ?
