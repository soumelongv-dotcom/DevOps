# DevOps

# Rapport de laboratoire : Conteneurisation et Orchestration

# Introduction

Ce rapport présente le travail effectué dans le cadre des laboratoires **Lab 7 – Conteneurs avec Docker et Lab 8 – Orchestration de conteneurs avec Kubernetes.**

Ces deux travaux pratiques ont pour objectif d’acquérir une compréhension concrète de la conteneurisation, du déploiement et de l’orchestration d’applications modernes à l’aide des technologies **Docker** et **Kubernetes.**

---

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

---

# Lab 8 : Orchestration de conteneurs avec Kubernetes

# Objectifs

- Installer et utiliser Minikube pour créer un cluster Kubernetes local.

- Manipuler les commandes kubectl.

- Créer, exposer, et faire évoluer un déploiement Kubernetes.

- Gérer plusieurs réplicas et versions d’une application.

- Déployer via des manifests YAML.

---

# 1. Installation de Minikube

Après installation, le cluster local a été démarré :
```bash
minikube start
minikube status
```
---

# 2. Découverte de kubectl

Un déploiement initial a été créé :
```bash
kubectl create deployment kubernetes-bootcamp \
--image=gcr.io/google-samples/kubernetes-bootcamp:v1
```

Les pods ont été listés :
```bash
kubectl get pods
kubectl logs <pod_name>
kubectl exec <pod_name> -- cat /etc/os-release
```

Un shell interactif a permis d’examiner les fichiers à l’intérieur du conteneur :
```bash
kubectl exec -it <pod_name> -- bash
```
---

# 3. Exposition du service

Le déploiement a été exposé à l’extérieur via un service de type NodePort :
```bash
kubectl expose deployments/kubernetes-bootcamp --type="NodePort" --port=8080
kubectl get services
minikube ip
```

L’application est devenue accessible via ``http://<minikube_ip>:<node_port>.``

---

# 4. Scalabilité

Le déploiement a été mis à l’échelle :
```bash
kubectl scale deployments/kubernetes-bootcamp --replicas=5
```

En actualisant la page web plusieurs fois, on a observé une répartition du trafic entre les différents pods (load balancing).
Une réduction du nombre de réplicas à 2 a été effectuée avec :
```bash
kubectl scale deployments/kubernetes-bootcamp --replicas=2
```

---

# 5. Mise à jour et gestion de versions

Les images ont été mises à jour successivement :
```bash
kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2
kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v3
```

Kubernetes a géré le **rolling update**, remplaçant progressivement les anciens pods.
L’opération a pu être annulée avec :
```bash
kubectl rollout undo deployments/kubernetes-bootcamp
```

---

# 6. Déploiement avec des fichiers YAML

Les fichiers ``deployment.yaml`` et ``service.yaml`` ont été complétés puis appliqués :
```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

Ensuite, le déploiement a été modifié pour contenir 3 réplicas, démontrant la montée en charge automatique et le routage transparent entre les pods.

Enfin, le nettoyage du cluster a été effectué :
```bash
kubectl delete service kubernetes-bootcamp
kubectl delete deployment kubernetes-bootcamp
minikube stop
```
---

# Bilan du Lab 8

- Maîtrise des commandes de base de **kubectl.**

- Compréhension du modèle de déploiement Kubernetes.

- Mise en œuvre de **la scalabilité horizontale**(réplicas).

- Application de **rolling updates** et **rollbacks.**

- Utilisation de fichiers YAML pour l’automatisation et la reproductibilité des déploiements.

---

# Conclusion Générale

Les laboratoires 7 et 8 ont permis de :

- Comprendre **la philosophie des conteneurs** et leur cycle de vie.

- Apprendre à créer, partager et exécuter des conteneurs via **Docker.**

- Découvrir le rôle de **Docker Compose** pour les applications multi-services.

- Explorer **Kubernetes** comme outil d’orchestration pour le déploiement, la mise à l’échelle et la gestion des conteneurs à grande échelle.

En somme, ces deux labs constituent **une transition complète du développement local à la mise en production** dans un environnement conteneurisé, illustrant les fondations de la modernisation des infrastructures logicielles.