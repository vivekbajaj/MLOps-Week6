# 🌸 Iris API - GKE Deployment with CI/CD

This repository contains the code and configuration for deploying a Machine Learning API (Iris classifier) using:

- Google Cloud Platform (GCP)
- Google Kubernetes Engine (GKE)
- GitHub Actions CI/CD
- Docker
- Cloud-based Machine Learning (CML) reporting

---

## 📁 Repository File Structure and Purpose

### ➤ `main.py`
- Entry point of the FastAPI application serving the machine learning model.
- Hosts `/predict/` and `/health` endpoints for API testing.

### ➤ `model.pkl`
- Serialized Iris classification model (likely trained using scikit-learn).
- Used by the API for making predictions.

### ➤ `Dockerfile`
- Defines the container image build process.
- Installs dependencies and runs the FastAPI server in a Docker container.

### ➤ `requirements.txt`
- Lists all Python packages required to run the application (e.g., FastAPI, scikit-learn, etc.).

### ➤ `deployment.yaml`
- Kubernetes deployment manifest.
- Specifies how the Docker image should be deployed on GKE.
- Includes container name, image, environment variables, replicas, etc.

### ➤ `service.yaml`
- Kubernetes service manifest.
- Exposes the deployed application as a LoadBalancer.
- Makes your API publicly accessible via external IP.

### ➤ `.github/workflows/deploy.yml`
- **GitHub Actions CI/CD pipeline**.
- Automates:
  - Checkout of code
  - Docker image build and push to Google Artifact Registry
  - Deployment to GKE cluster
  - Retrieval of external IP
  - API health check and testing
  - CML report generation with live predictions
  - Posting CML report as a GitHub comment or step summary

### ➤ `report.md` (Generated)
- Markdown file automatically created during CI/CD.
- Contains results from test predictions made on the deployed API.
- Used by CML to post deployment reports into GitHub.

---

## 🚀 Workflow Summary

Each push (or manual trigger) to the `main` branch:
1. Builds Docker image for the Iris API.
2. Pushes image to Google Artifact Registry.
3. Deploys the image to a GKE cluster using Kubernetes.
4. Waits for LoadBalancer IP and performs health checks.
5. Sends test predictions to the live API.
6. Generates a detailed CML report (`report.md`) with results.
7. Posts the report as a GitHub comment (**or fallback to job summary** if permissions are restricted).

---

## 📌 Notes

- Ensure your GitHub secrets (`GCP_PROJECT_ID`, `GCP_ARTIFACT_REPO`, `GCP_DOCKER_KEY`, `GKE_CLUSTER_NAME`, `GKE_ZONE`) are correctly set.
- The `gke-gcloud-auth-plugin` is required for authenticating `kubectl` with GKE in GitHub Actions.

---

🛠 Built with ❤️ by Vivek Bajaj 21F1002578
