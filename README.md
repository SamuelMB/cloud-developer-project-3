[![Build Status](https://travis-ci.org/SamuelMB/cloud-developer-project-3.svg?branch=master)](https://travis-ci.org/SamuelMB/cloud-developer-project-3)

# Udagram Cloud Developer Project 3

This is a cloud application developed for the Udacity Cloud Developer Nanodegree Program.

## Getting Started

### Local Deployment

These tools must be installed on your machine:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

Ensure that the following variables are set in your environment:

    POSTGRES_USERNAME
    POSTGRES_PASSWORD
    POSTGRES_DB
    POSTGRES_HOST
    AWS_REGION
    AWS_PROFILE
    AWS_BUCKET
    JWT_SECRET

Build docker images:

```
docker-compose -f docker-compose-build.yaml build --parallel
```

Start up containers and services:

```
docker-compose -f docker-compose.yaml up
```

If you want that containers runs with detached mode:

```
docker-compose -f docker-compose.yaml up -d
```

### Kubernetes Deployment

These tools must be installed on your machine:

- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [Kubeone](https://github.com/kubermatic/kubeone)
- [Terraform](https://learn.hashicorp.com/terraform/getting-started/install.html)

Follow this guide from Kubeone to provision and setup kubernetes on AWS:

- https://github.com/kubermatic/kubeone/blob/master/docs/quickstart-aws.md 

All kubernetes sources stored in the following folders:

- ./reverseproxy/k8s
- ./udacity-c3-frontend/k8s
- ./udacity-c3-restapi-feed/k8s
- ./udacity-c3-restapi-user/k8s

Replace all variables in secrets and configmap files.

Apply k8s files:

```
# Deploy REST API User
kubectl apply -f udacity-c3-restapi-user/k8s/configmap.yaml
kubectl apply -f udacity-c3-restapi-user/k8s/secret.yaml
kubectl apply -f udacity-c3-restapi-user/k8s/service.yaml
kubectl apply -f udacity-c3-restapi-user/k8s/deployment.yaml

# Deploy REST API Feed
kubectl apply -f udacity-c3-restapi-feed/k8s/configmap.yaml
kubectl apply -f udacity-c3-restapi-feed/k8s/secret.yaml
kubectl apply -f udacity-c3-restapi-feed/k8s/aws-auth-secret.yaml
kubectl apply -f udacity-c3-restapi-feed/k8s/service.yaml
kubectl apply -f udacity-c3-restapi-feed/k8s/deployment.yaml

# Deploy ReverseProxy
kubectl apply -f reverseproxy/k8s/service.yaml
kubectl apply -f reverseproxy/k8s/deployment.yaml

# Deploy Frontend
kubectl apply -f udacity-c3-frontend/k8s/service.yaml
kubectl apply -f udacity-c3-frontend/k8s/deployment.yaml
```
