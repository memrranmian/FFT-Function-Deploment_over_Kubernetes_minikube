# PC Restart & Redeployment Guide

If you have restarted your PC and need to start all over again, follow these sequential steps to get your environment and application back up and running:

## Step 1: Start Minikube & Tunnel
1. Open your terminal (or WSL Ubuntu terminal).
2. Start your local Kubernetes cluster:
   ```bash
   minikube start
   ```
3. Open a tunnel in a separate terminal window to route LoadBalancer IPs:
   ```bash
   minikube tunnel
   ```

## Step 2: Apply Kubernetes Configurations
1. Navigate to the directory containing your configuration files.
2. Apply the deployment configuration:
   ```bash
   kubectl apply -f fft-deployment.yaml
   ```
3. Apply the service and HPA configuration:
   ```bash
   kubectl apply -f fft-hpa-lb.yaml
   ```

## Step 3: Verify Pods and Services
1. Check that your pods are running successfully:
   ```bash
   kubectl get pods
   ```
2. Check your services to get the external IP address:
   ```bash
   kubectl get svc
   ```

## Step 4: Run Load Testing
1. Use `httperf` against your service endpoint to test autoscaling behavior:
   ```bash
   httperf --server 127.0.0.1 --port 80 --uri /index.php --num-conns 300 --rate 1500
   ```
2. Monitor the autoscaling behavior via the Kubernetes dashboard (`minikube dashboard`) or by watching pod replicas:
   ```bash
   kubectl get hpa --watch
   ```