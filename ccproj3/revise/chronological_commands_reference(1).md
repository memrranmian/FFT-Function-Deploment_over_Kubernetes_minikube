# Comprehensive Chronological Command Reference

This document outlines the complete sequence of commands and setup procedures executed throughout the project, starting from the foundational environment setup (Docker, WSL, and Minikube installation) through to cluster deployment, load testing, and verification.

---

## Phase 1: Environment Setup & Prerequisites

### 1. Verify or Update WSL (Windows Subsystem for Linux)
```bash
wsl --update
```
* **Description:** Ensures WSL is up to date to provide a stable Linux environment on Windows for running Docker and Kubernetes.

### 2. Install/Verify Docker Desktop integration with WSL
* **Description:** Docker Desktop is configured to integrate with the WSL backend, allowing containers to run seamlessly inside the Linux subsystem.

### 3. Install Minikube
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
* **Description:** Downloads and installs the Minikube binary inside the WSL Ubuntu environment to provision a local single-node Kubernetes cluster.

---

## Phase 2: Cluster Initialization & Networking

### 4. Start Minikube Cluster
```bash
minikube start
```
* **Description:** Initializes the local Kubernetes cluster, configured to use Docker as the container driver.

### 5. Open Minikube Tunnel
```bash
minikube tunnel
```
* **Description:** Establishes a network route from the host machine to services of type `LoadBalancer`, enabling local external IP accessibility.

---

## Phase 3: Application Deployment & Configuration

### 6. Check Active Pods & Deployment Status
```bash
kubectl get pods
```
* **Description:** Lists current pods and checks their health indicators (e.g., verifying running status or transitional orange states).

### 7. Check Services & External IPs
```bash
kubectl get svc
```
* **Description:** Verifies the LoadBalancer service and retrieves its assigned external IP address for accessing the application.

### 8. Apply Deployment Configuration
```bash
kubectl apply -f fft-deployment.yaml
```
* **Description:** Deploys the FFT application pods onto the Kubernetes cluster based on the configuration file.

### 9. Apply Service and HPA Configuration
```bash
kubectl apply -f fft-hpa-lb.yaml
```
* **Description:** Sets up the LoadBalancer and the Horizontal Pod Autoscaler (HPA) configured with a 30% CPU utilization threshold.

---

## Phase 4: Load Testing & Verification

### 10. Execute Load Test with httperf
```bash
httperf --server 127.0.0.1 --port 80 --uri /index.php --num-conns 300 --rate 1500
```
* **Description:** Simulates traffic load against the FFT application endpoint to push CPU utilization past the 30% threshold and trigger autoscaling.

### 11. Monitor Autoscaling Behavior
```bash
kubectl get hpa --watch
```
* **Description:** Continuously tracks the scaling metrics and replica count changes (scaling up to the maximum of 5 pods) in real-time.