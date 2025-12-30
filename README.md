# Simple DevOps CI/CD Pipeline
----------------------------
A minimal, end-to-end pipeline to demonstrate Continuous Integration (CI) and Container Orchestration.

## Pipeline Architecture
1. **Code**: Python Flask app logic in `app.py`.
2. **Containerize**: `Dockerfile` packages the app and dependencies.
3. **Continuous Integration**: **GitHub Actions** builds the image and pushes it to **Docker Hub** on every push to `main`.
4. **Orchestration**: **Kubernetes** (Docker Desktop) manages the deployment, scaling, and networking.
5. **Continuous Deployment**: Managed via Kubernetes manifests (GitOps-ready).


## Project Structure

app.py: Flask web application.

Dockerfile: Instructions for building the Docker image.

.github/workflows/ci.yml: Automation script for GitHub Actions.

k8s/deployment.yaml: Defines the desired state (4 pods).

k8s/service.yaml: Exposes the app to your browser.

## Setup & Run
1. Build and Run Locally (Docker)
```
docker build -t simple-app .
docker run -p 5000:5000 simple-app
```
3. Deploy to Kubernetes
```
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```
3. Verify the Pods
```
kubectl get pods
kubectl get svc
```
4. Access the App

If the LoadBalancer stays "pending," use a port-forward to see the app:
```
kubectl port-forward pod/<your-pod-name> 5005:5000
```
Visit http://localhost:5005 in the browser.
