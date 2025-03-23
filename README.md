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
Dockerfile de l'API
Le Dockerfile de l'API est construit à partir de l'image Python 3.8 et inclut:

 - Installation des dépendances système nécessaires
 - Configuration d'un volume pour les données persistantes
 - Exposition du port 5000
 - Configuration de l'authentification basique

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
Ce fichier configure deux services:
 - API - Le backend Python/Flask
 - Website - Le frontend PHP
#### Étapes :
1. Modifier `index.php` pour configurer l'URL de l'API
2. Lancer les services avec Docker Compose :
```sh
docker-compose up -d
```

![build image from DockerFile ](screenDocker/file.png)
3. Accéder à l'application :
   - **API** : `http://localhost:5000`
   - **Interface Web** : `http://localhost:8080`

---
### 3. Docker Compose Registry
docker-compose-registry.yml
Ce fichier déploie:
 - Un *registre Docker privé* pour stocker les images
 - Une *interface web* pour visualiser et gérer les images dans le registre

#### Étapes :
1. Déployer le registre privé avec :  
   Avant de commencer, il faut lancer le registre Docker privé avec **Docker Compose**.
   
     ![Déployer le registre privé  ](screenDocker/dockerReg.png)
   
3. Ajouter le tag  
    Avant d’envoyer une image vers notre registre privé, nous devons lui attribuer un tag correspondant à l’URL du registre.
      ![Ajouter le tag de notre image   ](screenDocker/tag.png)
   
    **Explication** :  
       -student_api : Nom de l’image Docker créée  
       -localhost:5001/student_api : Tag pour associer l’image à notre registre privé  
   
4. Pousser l'image crée vers le registre privé :  
    Maintenant que l’image a un tag, nous pouvons l’envoyer vers notre registre privé.  
     ![Pousser notre image   ](screenDocker/pushRegist.png)   

5. tester la présence de notre image  en registre privé :   
    Une fois l’image poussée, nous pouvons vérifier qu’elle est bien stockée dans le registre privé avec :   
   
      ![tester notre image   ](screenDocker/testReg.png)  

 ## Conclusion
Grâce à ces étapes, vous avez maintenant un registre Docker privé opérationnel où vous pouvez stocker et gérer vos images localement. Vous pouvez également utiliser l'interface web associée pour naviguer plus facilement parmi les images disponibles.

## Auteurs
- **Mohammed Reda kadiri**
- **Ayoub Jarhni**
- **Zakaria El hajjam**

---
## Licence
Ce projet est sous licence MIT.

