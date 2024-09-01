# DevOps Final Project

## Project Overview
This project involved developing a CI/CD pipeline for a microservices architecture on AWS. It included deploying two Telegram chatbots, which process images through a series of services: receiving images from Telegram, placing them into S3 bucket and SQS queue, processing them with YOLOv5 for object detection, storing results in DynamoDB, and sending the detections back to the Telegram user. The application ran on a Kubernetes cluster with two EC2 nodes—one for the control plane and one for the worker node. The CI/CD pipeline, managed with Jenkins and ArgoCD, automated build, test, and deployment processes. Jenkins handled code changes and releases, while ArgoCD deployed updates to the Kubernetes cluster, ensuring seamless integration and delivery.

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
