# Chronological Command Reference

This document outlines all the commands used throughout the assignment sessions in chronological order, along with a description of their purpose.

## 1. Cluster & Environment Initialization

### Start Minikube Cluster
```bash
minikube start
```
* **Description:** Initializes the local Kubernetes cluster inside Docker/WSL to begin working with nodes and resources.

### Open Minikube Tunnel
```bash
minikube tunnel
```
* **Description:** Creates a network route to services running of type `LoadBalancer`, allowing local access to cluster endpoints from the Windows/WSL host machine.

---

## 2. Deployment & Resource Management

### Check Existing Pods
```bash
kubectl get pods
```
* **Description:** Lists all running and transitional pods in the active namespace to verify container health, status, and replica count.

### Check Services & External IP
```bash
kubectl get svc
```
* **Description:** Displays services and their assigned cluster or external IP addresses, verifying the LoadBalancer setup.

### Apply Deployment Configuration
```bash
kubectl apply -f fft-deployment.yaml
```
* **Description:** Creates or updates the Kubernetes deployment resource that manages the FFT application pods.

### Apply Service & HPA Configuration
```bash
kubectl apply -f fft-hpa-lb.yaml
```
* **Description:** Deploys or updates the LoadBalancer service and the Horizontal Pod Autoscaler (HPA) configured with a 30% utilization threshold.

---

## 3. Load Testing & Monitoring

### Execute Load Test with httperf
```bash
httperf --server 127.0.0.1 --port 80 --uri /index.php --num-conns 300 --rate 1500
```
* **Description:** Simulates high traffic volume against the application endpoint to test resource consumption and trigger the HPA scale-up behavior.

### Watch HPA Status
```bash
kubectl get hpa --watch
```
* **Description:** Continuously monitors the Horizontal Pod Autoscaler metrics (such as current vs. target CPU utilization and replica counts) in real-time as load is applied.