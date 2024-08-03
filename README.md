# DevOps Final Project

## Project Overview
This project demonstrates a CI/CD pipeline for a microservices architecture deployed in a Kubernetes cluster on AWS. The pipeline includes automated build, test, and deployment processes for both development and production environments, using Jenkins and ArgoCD for continuous integration and continuous delivery.

## Prerequisites
Nodes/EC2 Instances
* Node 1 (Control Plane): Ubuntu-based image, minimum 4GB RAM, 2 CPUs.
* Node 2 (Worker Node): Ubuntu-based image, minimum 4GB RAM, 2 CPUs.

## Setup Steps
### 1.Main Node (Control Plane) Setup

  * Install kubeadm, kubelet, and kubectl.
  * Configure the cluster with kubeadm init.
  * Install Flannel as the CNI to enable communication between pods.
  * Join the Worker Node to the cluster using the join command from kubeadm.

### 2.Worker Node Setup

  * Install kubeadm, kubelet, and kubectl.
  * Join the cluster using the token and hash from the Control Plane setup.

## Architecture Overview

### Kubernetes Cluster
* Control Plane Node
 * Runs kube-apiserver, etcd, kube-scheduler, kube-controller-manager, and cloud-controller-manager.
 * Handles overall cluster management.

### Worker Nodes
* Runs kubelet and kube-proxy.
* Hosts application pods.

### Application Components
* Telegram Bots
  * Two bots: one for development, one for production.
* Microservices
  * yolo5 and polybot apps deployed in both dev and prod environments.
  * Monitored using Prometheus and Grafana.

### Pipelines
* CI/CD Pipelines
  * Three pipelines per environment (dev and prod):
   * yolo5 build pipeline.
   * polybot build pipeline.
   * Release pipeline.
* Uses Jenkins for automation.
* Utilizes ArgoCD for deployment.


# Usage
After completing the setup and installation, access your applications through the configured domain and monitor their performance and logs using Grafana and Prometheus dashboards. ArgoCD will continuously monitor your Git repository for changes and automatically synchronize the desired state with your Kubernetes cluster.
