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
├── backend/
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── student_age.py
│   ├── student_age.json
│
├── frontend/
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
```sh
docker build -t student_api ./backend
```
2. Lancer le conteneur :
```sh
docker run -d -p 5000:5000 -v $(pwd)/backend/student_age.json:/data/student_age.json student_api
```
3. Tester l'API :
```sh
curl -X GET http://localhost:5000/SUPMIT/api/v1.0/get_student_ages
```

---
### 2. Déploiement avec Docker Compose
1. Modifier `index.php` pour configurer l'URL de l'API
2. Lancer les services avec Docker Compose :
```sh
docker-compose up -d
```
3. Accéder à l'application :
   - **API** : `http://localhost:5000`
   - **Interface Web** : `http://localhost:8080`

---
### 3. Docker Registry
1. Déployer le registre privé avec :
```sh
docker-compose -f docker-compose-registry.yml up -d
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
- **Votre Nom**
- **Email de contact**

---
## Licence
Ce projet est sous licence MIT.

