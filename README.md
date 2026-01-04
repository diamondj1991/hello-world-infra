# Hello World Infrastructure (GitOps)

This repository contains the Infrastructure-as-Code (IaC) required to deploy the Hello World application to a Kubernetes cluster using **Helm** and **ArgoCD**.

## 🏗️ Architecture
This project follows **GitOps** principles. Any changes pushed to this repository are automatically detected and synchronized to the cluster by ArgoCD.

- **Orchestration:** Kubernetes (Minikube)
- **Deployment:** Helm (3 Replicas for High Availability)
- **Ingress:** Nginx Ingress Controller (`hello-world.local`)
- **CD/GitOps:** ArgoCD



## 📁 Repository Structure
- `/charts`: Contains the `hello-world-app` Helm chart.
- `values.yaml`: The "Source of Truth" for environment-specific configurations (image tags, replica counts, etc.).

## 🚀 Deployment Guide

### 1. Initial Setup
1. Ensure Minikube is running with the Ingress addon: `minikube addons enable ingress`
2. Install ArgoCD in the `argocd` namespace.

### 2. Connect the App to ArgoCD
Create a new application in ArgoCD pointing to this repository. Set the sync policy to `Automatic`.

### 3. Local Access (WSL2 Note)
Due to the nature of the WSL2/Docker bridge, run the following to access the Ingress:
1. Start the tunnel: `minikube tunnel`
2. Add the IP to your hosts file: `192.168.49.2 hello-world.local`
3. If traffic hangs, validate the internal route via `minikube ssh`.

## 🛡️ Security & Enterprise Improvements
In a production environment, this deployment would be enhanced with:
- **Secrets Management:** Integration with HashiCorp Vault.
- **Network Policies:** Restricting pod-to-pod communication.
- **RBAC:** Scoped permissions for the ArgoCD service account.
