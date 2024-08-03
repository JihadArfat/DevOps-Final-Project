# DevOps Final Project

## Project Overview
This project demonstrates a CI/CD pipeline for a microservices architecture deployed in a Kubernetes cluster on AWS. The pipeline includes automated build, test, and deployment processes for both development and production environments, using Jenkins and ArgoCD for continuous integration and continuous delivery.

## Prerequisites
* AWS account with necessary permissions
* kubectl installed
* Helm installed
* Jenkins installed and configured
* ArgoCD installed and configured

## Architecture

* Frontend Microservice: Customer-facing service.
* Database: Managed by AWS (e.g., DynamoDB).
* Background Microservices: Handle various backend tasks.
* Communication: Both synchronous (HTTP request/response) and asynchronous (queues or topics).

## Setup and Installation
### Kubernetes Cluster on AWS

1. Create EKS Cluster:

* Create an EKS cluster using AWS Management Console or CLI.
*  Configure kubectl to connect to the EKS cluster.

2. Install Container Runtime:

* Install required tools: jq and awscli.
*  Choose and install a container runtime (e.g., cri-o or containerd).

3. Initialize Control Plane Node:

* Create IAM role with necessary permissions.
* Set up security groups and EC2 instance.
* Install kubeadm, kubelet, and kubectl.
* Initialize the cluster with kubeadm init.


# Usage
After completing the setup and installation, access your applications through the configured domain and monitor their performance and logs using Grafana and Prometheus dashboards. ArgoCD will continuously monitor your Git repository for changes and automatically synchronize the desired state with your Kubernetes cluster.
