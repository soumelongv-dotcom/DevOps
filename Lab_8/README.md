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