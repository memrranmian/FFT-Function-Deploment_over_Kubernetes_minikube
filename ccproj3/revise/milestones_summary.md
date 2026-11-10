# Kubernetes Autoscaling and FFT Milestone Summary

We have successfully completed all three milestones for this project:

1. **Milestone 1: Deployment & Service Setup**
   - Deployed the FFT application containers using Kubernetes.
   - Configured a LoadBalancer service to expose the application externally.

2. **Milestone 2: Horizontal Pod Autoscaler (HPA)**
   - Configured HPA to automatically scale the deployment based on CPU utilization.
   - Adjusted thresholds (e.g., CPU average utilization target) to observe dynamic scaling up to the maximum limit of 5 replicas.

3. **Milestone 3: Load Testing & Verification**
   - Executed load testing tools like `httperf` to simulate heavy traffic against the service IP (`127.0.0.1` or the assigned external IP).
   - Verified that the HPA successfully detects the load, increases replica counts, and processes requests correctly, with output matching expected FFT and inverse FFT calculations.