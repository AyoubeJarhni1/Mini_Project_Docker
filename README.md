# Mini-Projet : Conteneurisation d'une Application avec Docker

## Description
Ce projet a pour objectif de conteneuriser une application existante en utilisant Docker. L'application comprend :
- Un backend en **Python** utilisant **Flask**
- Un frontend en **PHP** permettant l'affichage des étudiants

Le but est d'améliorer le déploiement et l'évolutivité de l'application en utilisant **Docker** et **Docker Compose**.

---
## Objectifs du Projet
### Objectifs Pratiques :
- **Maîtriser Docker** : Construire et exécuter des conteneurs
- **Gestion des versions** : Versionner les images et gérer leur stockage
- **Infrastructure as Code (IaC)** : Automatiser le déploiement avec Docker Compose
- **Sécurité** : Assurer un déploiement sécurisé

---
## Contexte
SUPMIT, une entreprise de développement de logiciels pour les universités, souhaite améliorer son infrastructure afin de garantir une meilleure automatisation et évolutivité.

L'application existante fonctionne actuellement sur un serveur unique et nécessite une solution conteneurisée pour améliorer l'agilité du déploiement.

---
## Infrastructure
- Un serveur avec **Docker** installé
- Deux services conteneurisés :
  - **API REST (Flask)** : Gère et retourne la liste des étudiants
  - **Application web (PHP)** : Interface utilisateur permettant d'afficher la liste des étudiants
- **Un registre Docker privé** pour stocker les images créées

---
## Structure du Projet
```
.
├── simple_api/
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── student_age.py
│   ├── student_age.json
│
├── website/
│   ├── index.php
│
├── docker-compose.yml
├── docker-compose-registry.yml
├── README.md
```

---
## Installation et Déploiement
### 1. Construire et Tester l'API
#### Étapes :
1. Construire l'image Docker :

![build image from DockerFile](screenDocker/file.png)

Explication ::
En utilisant cette commande on construit l'image à partir du dockerFile qu'on a crée 

2. Lancer le conteneur :
![lancer le conteneur à partir de l'image ](screenDocker/runImage.PNG)
Explication ::: 
cette commande nous permet d'exécuter un conteneur à partir de notre image construite "student_api"
3. Tester l'API :

![Tester l'API à travers le conteneur  ](screenDocker/testDF.png)

EXPLICATION :
Cette commande nous permet de tester l'API , et voilà le résultat est réussi .   
---
### 2. Déploiement avec Docker Compose

Docker Compose est un outil puissant qui permet de définir et de gérer des applications multi-conteneurs Docker à l'aide d'un fichier YAML (`docker-compose.yml`). Cette solution :

- Simplifie considérablement le déploiement d'applications complexes
- Automatise la création, la configuration et l'orchestration des conteneurs
- Facilite le développement et les tests dans des environnements reproduisibles
- Permet de définir l'ensemble de l'infrastructure comme du code


#### 2.1 Description des services

##### Service API (supmit_api)
- Basé sur l'image personnalisée `student-api`
- Expose le port 5000 pour les requêtes API
- Monte un volume local contenant le fichier `student_age.json` pour la persistance des données
- S'exécute dans le réseau `mynetwork`

##### Service Web (website)
- Utilise l'image officielle `php:apache` pour héberger un site web
- Variables d'environnement prédéfinies (`USERNAME` et `PASSWORD`) pour l'authentification
- Dépend du service API (s'assure que l'API démarre d'abord)
- Expose le site sur le port 8081
- Monte les fichiers du projet via un volume local
- Partage le même réseau que l'API pour permettre la communication inter-services

#### 2.2 Lancement des conteneurs

Pour démarrer l'ensemble de l'infrastructure, on a utiliser la commande suivante à la racine du projet :

```bash
docker-compose up --build
```

L'option `--build` permet de reconstruire les images si nécessaire avant de lancer les conteneurs.

#### 2.3 Accès à l'interface web

Une fois l'application déployée, on a accéder au partie front end :

- URL : `http://localhost:8081`
- Affiche les données des étudiants stockées dans le fichier JSON

![Interface web PHP](screenDocker/check.png)
*Liste des étudiants affichée par l'interface web PHP*







### 3. Docker Registry
1. Déployer le registre privé avec :
```sh
docker-compose -f docker-compose-registry.yml up 
```
2. Ajouter le tag et pousser l'image :
```sh
docker tag student_api localhost:5000/student_api

docker push localhost:5000/student_api
```

---
## Captures d'Écran
Ajoutez ici des captures d'écran des tests de votre API et interface web.

---
## Auteurs
- **Mohammed Reda kadiri**
- **Ayoub Jarhni**
- **Zakaria El hajjam**

---
## Licence
Ce projet est sous licence MIT.

