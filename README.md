# Fullstack Nodejs  with K8S

This repository contains a application that includes a frontend, backend, and MongoDB database. Everything is deployed using Kubernetes.

## Getting Started

### Prerequisites

- Docker
- Kubernetes (Minikube)
- kubectl

### Build and Push Docker Images

Build and push the docker images to docker hub for both frontend and backend.

```bash
# Backend
cd backend
docker build -t DOCKER_USERNAME/napp-backend:1.1 .
docker tag napp-backend:1.1 DOCKER_USERNAME/napp-backend:1.1

docker push DOCKER_USERNAME/napp-backend:1.1

# Frontend
cd ../frontend
docker build -t DOCKER_USERNAMEnginx-frontend:1.1 .
docker tag nginx-frontend:1.1 DOCKER_USERNAME/nginx-frontend:1.1
docker push DOCKER_USERNAME/nginx-frontend:1.1
```

### Deploy to K8s Manifests
```bash
## Create the namespace
kubectl create namespace fullstack-app

## K8s files directory
cd K8s-files

## Deploy Config map
kubectl apply -f configMap.yaml -n fullstack-app

## Deploy Persistent Volume and persistent Volume Claim
kubectl apply -f pervolume.yaml -n fullstack-app

## Deploy Secret
kubectl apply -f secret.yaml -n fullstack-app

## Deploy MongoDB
cd mongodb
kubectl apply -f deployment.yaml -n fullstack-app
kubectl apply -f service.yaml -n fullstack-app

## Deploy Node.js backend
cd ../nodejs
kubectl apply -f deployment.yaml -n fullstack-app
kubectl apply -f service.yaml -n fullstack-app


## Deploy Nginx frontend
cd ../nginx
kubectl apply -f deployment.yaml -n fullstack-app
kubectl apply -f service.yaml -n fullstack-appkubectl apply -f K8s-files/Nginx/ -n fullstack-app
```

### Verify Deployments
Ensure all pods & deployments are running correctly:

```bash
kubectl get deployments -n fullstack-app

kubectl get pods -n fullstack-app
```
### Access the frontend

```bash
kubectl get svc -n fullstack-app
minukube ip
```
Application URL: **<minikubeip>:<node-port-nginx>**


### Rolling Updates

```bash
kubectl set image deployment/nginx-frontend-deployment nginx-frontend=DOCKER_USERNAME/nginx-frontend:1.2 -n fullstack-app
```

## App Scalling

### Frontend Scalling
```bash
kubectl sclade deployment/nginx-frontend-deployment --replicas=5 -n fullstack-app
```

### Backned Scalling
```bash
kubectl sclade deployment/napp-back-deployment --replicas=3 -n fullstack-app
```

## App Logs

```bash
kubectl logs deployment/napp-backend-deployment -n fullstack.app
```
or for detailed information
```bash
kubectl descrie deployment napp-backend-deployment -n fullstack.app