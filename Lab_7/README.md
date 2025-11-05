# Lab 7 : Conteneurs avec Docker

**Objectifs**

- Installer et configurer Docker Desktop.

- Créer un Dockerfile pour conteneuriser une application Node.js.

- Exécuter, gérer et partager un conteneur Docker.

- Créer une application multi-conteneurs à l’aide de Docker Compose.

- Comprendre la persistance des données via les volumes Docker.

---

# 1. Installation de Docker

L’installation de Docker Desktop a été réalisée selon le système d’exploitation utilisé.
Une fois installé, la commande suivante a permis de vérifier le bon fonctionnement :

```bash 
docker run hello-world
```

---

# 2. Création d’une image Docker

Dans le répertoire ``lab/hello-world-docker``, l’application Node.js « Hello World » a été examinée.

Elle contient les fichiers :

- ``server.js``: code source Node.js

- ``package.json`` : dépendances et métadonnées

- ``Dockerfile`` : instructions de création du conteneur

Notre dossier **Dockerfile** :
```bash
FROM node:12

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 8080

CMD [ "npm", "start" ]
```

L’image a été construite à l’aide de la commande :
```bash
docker build -t hello-world-docker .
```

et vérifiée avec :
```bash
docker images
```
---

# 3. Exécution et gestion du conteneur

Le conteneur a été exécuté avec le port 8080 exposé sur le port 12345 de la machine hôte :
```bash
docker run -p 12345:8080 -d hello-world-docker
```

Les commandes suivantes ont permis de gérer le conteneur :
```bash
docker ps              # Affiche les conteneurs actifs
docker logs <ID>       # Affiche les journaux
docker stop <ID>       # Arrête un conteneur
```

L’application a été accessible à l’adresse :
``http://localhost:12345``

---

# 4. Partage sur Docker Hub

Le fichier ``server.js`` a été modifié pour personnaliser le message (« Hello World from Docker! I have been seen! »).
Une nouvelle image a été créée, puis publiée sur *Docker Hub* :
```bash
docker tag hello-world-docker <dockerhub_user>/<image_name>
docker login
docker push <dockerhub_user>/<image_name>
```

Un camarade de classe a pu télécharger et exécuter cette image avec :
```bash
docker pull <dockerhub_user>/<image_name>
docker run -p 12345:8080 -d <dockerhub_user>/<image_name>
```

---

# 5. Application multi-conteneurs avec Docker Compose

Dans le répertoire ``lab/hello-world-docker-compose``, une version plus complexe de l’application a été créée.
Elle se compose :

- D’un conteneur Node.js (serveur web)

- D’un conteneur Redis (base de données en mémoire)

Notre fichier docker-compose.yaml :

```bash
version: '3'
services:
  redis:
    image: redis
  web:
    # COMPLETE HERE
    depends_on:
      - redis
    build: .
    ports:
      - "5000:8080"
    environment:
      - REDIS_HOST=redis
      - REDIS_PORT=6379    
```

Les commandes principales :
```bash
docker-compose up
docker-compose rm
```

Lors du redémarrage sans volume, le compteur Redis a été remis à zéro.
L’utilisation d’un volume Docker a permis de **préserver l’état des données entre les exécutions.**

---

# Bilan du Lab 7

- Concept d’image et de conteneur.

- Maîtrise des commandes Docker de base.

- Publication d’une image sur Docker Hub.

- Mise en place d’une architecture multi-conteneurs.

- Introduction à la persistance des données avec les volumes.