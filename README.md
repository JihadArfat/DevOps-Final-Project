# DevOps Final Project
## Project Objective
Design and implement a comprehensive CI/CD pipeline for a service deployed in a microservices architecture within Kubernetes.

# Table of Contents

## Project Overview

Prerequisites
Architecture
Setup and Installation
Kubernetes Cluster on AWS
Ingress-Nginx
ArgoCD
CI/CD with Jenkins
Monitoring with Grafana and Prometheus
Usage
Project Structure
Contributing
License

## Project Overview
This project demonstrates a CI/CD pipeline for a microservices architecture deployed in a Kubernetes cluster on AWS. The pipeline includes automated build, test, and deployment processes for both development and production environments, using Jenkins and ArgoCD for continuous integration and continuous delivery.

## Prerequisites

AWS account with necessary permissions
kubectl installed
Helm installed
Jenkins installed and configured
ArgoCD installed and configured

# Architecture
Frontend Microservice: Customer-facing service.
Database: Managed by AWS (e.g., RDS).
Background Microservices: Handle various backend tasks.
Communication: Both synchronous (HTTP request/response) and asynchronous (queues or topics).
Setup and Installation
Kubernetes Cluster on AWS
Create EKS Cluster:

Create an EKS cluster using AWS Management Console or CLI.
Configure kubectl to connect to the EKS cluster.
Install Container Runtime:

Install required tools: jq and awscli.
Choose and install a container runtime (e.g., cri-o or containerd).
Initialize Control Plane Node:

Create IAM role with necessary permissions.
Set up security groups and EC2 instance.
Install kubeadm, kubelet, and kubectl.
Initialize the cluster with kubeadm init.
Ingress-Nginx
Install Ingress-Nginx using Helm:

bash
نسخ الكود
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install ingress-nginx ingress-nginx/ingress-nginx
ArgoCD
Install ArgoCD:

bash
نسخ الكود
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
Access ArgoCD:

bash
نسخ الكود
kubectl port-forward svc/argocd-server -n argocd 8080:443
Login to ArgoCD:

bash
نسخ الكود
argocd login <ARGOCD_SERVER>
Create Application:

bash
نسخ الكود
argocd app create <APP_NAME> --repo <REPO_URL> --path <PATH_TO_MANIFESTS> --dest-server https://kubernetes.default.svc --dest-namespace <NAMESPACE>
Sync Application:

bash
نسخ الكود
argocd app sync <APP_NAME>
CI/CD with Jenkins
Create Folders:

Create dev and prod folders in Jenkins.
Build Pipelines:

Implement build pipelines for each microservice for both dev and prod environments.
Release Pipelines:

Implement release pipelines that update Kubernetes manifests and trigger ArgoCD deployments.
Monitoring with Grafana and Prometheus
Install Grafana and Prometheus using Helm:

bash
نسخ الكود
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/kube-prometheus-stack

# Usage
After completing the setup and installation, access your applications through the configured domain and monitor their performance and logs using Grafana and Prometheus dashboards. ArgoCD will continuously monitor your Git repository for changes and automatically synchronize the desired state with your Kubernetes cluster.
