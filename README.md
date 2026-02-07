# Kubernetes Orchestration Workflow

A hands-on project demonstrating how to containerize a FastAPI application and deploy it on Kubernetes using Docker, Minikube, and kubectl. Covers the full workflow from local development to scalable, service-backed deployment with clear operational commands.

📘 For a detailed breakdown, refer to this guide: [Kubernetes Workflow Commands](https://azure-lamb-4e6.notion.site/Kubernetes-Project-Workflow-Commands-Mental-Model-300db05ef512803c9e6ee62c328e5c85)

<br>

<p align="center">
  <a href="https://www.python.org/">
    <img src="https://img.shields.io/badge/Python-white?logo=python" alt="Python" />
  </a>
  <a href="https://uv.sh/">
    <img src="https://img.shields.io/badge/UV-white?logo=uv" alt="uv" />
  </a>
  <a href="https://fastapi.tiangolo.com/">
    <img src="https://img.shields.io/badge/FastAPI-white?logo=fastapi" alt="FastAPI" />
  </a>
  <a href="https://www.docker.com/">
    <img src="https://img.shields.io/badge/Docker-white?logo=docker" alt="Docker" />
  </a>
  <a href="https://kubernetes.io/">
    <img src="https://img.shields.io/badge/Kubernetes-white?logo=kubernetes" alt="Kubernetes" />
  </a>
  <a href="https://opensource.org/licenses/MIT">
    <img src="https://img.shields.io/badge/License-MIT-informational" alt="License" />
  </a>
</p>


---

## 📂 Project Structure

```text
fastapi-k8s-orchestration/
│
├─ src/
│   ├─ static/
│   │   └─ style.css      # CSS styles for the frontend UI
│   ├─ templates/
│   │   └─ index.html     # HTML template rendered by FastAPI (Jinja2)
│   └─ app.py             # FastAPI application entry point
│
├─ k8s/
│   ├─ deployment.yaml    # Kubernetes Deployment (pods, replicas, image, resources)
│   └─ service.yaml       # Kubernetes Service (exposes pods inside/outside cluster) 
│
├─ pyproject.toml         # Dependency declaration (uv-managed)
├─ uv.lock                # Locked dependencies for reproducibility
├─ Dockerfile             # Docker container configuration
├─ K8s_IN_PRODUCTION.md   # Kubernetes in real-world production environments
├─ README.md
├─ .gitignore
└─ .venv
```

---

## 🛠️ Tech Stack

- **Python 3.13**
- **FastAPI** – REST API and server-side rendering
- **UV** – Fast, reproducible dependency management
- **Docker** – Containerization and image management
- **Kubernetes** – Container orchestration, scaling, and service exposure

---

## 📦 Prerequisites

Choose the setup based on how you want to run the application.

**Option 1: Running Locally (Without Docker)**

- Python 3.13
- [uv](https://uv.sh/) package manager
- Git

> This is only required if you want to run the API directly on your host machine.

**Option 2: Using Docker**

- Docker installed on your system.

> No need to install Python, uv, or packages locally. Docker contains everything.

**Option 3: Using Kubernetes (Minikube)**

- Docker
- Minikube
- kubectl

> Recommended if you want to test container orchestration, scaling, and service exposure locally using Kubernetes.
> Modify `deployment.yaml` and `service.yaml` file in k8s folder (if needed)

---

## 🚀 Quick Start Guide

#### 1. Clone the repository

```bash
git clone https://github.com/arpon-kapuria/fastapi-k8s-orchestration.git
cd fastapi-k8s-orchestration
```

#### 2. Install dependencies

```bash
# Using uv package manager
uv sync --locked

# This creates a .venv and installs all required packages.
```

#### 3. Run Locally (Without Docker)

```bash
# Run the FastAPI application locally 
uv run uvicorn src.predict:app --host 0.0.0.0 --port 9696 --reload

# --host 0.0.0.0 makes it accessible from all network interfaces
# --port 9696 sets the port to 9696
# --reload enables automatic server reload when code changes
```

#### 4. Run with Docker

```bash
# Build the Docker image
docker build -t fastapi-k8s-orchestration .

# Run the container (the --rm flag deletes the container automatically after it stops)
docker run -it --rm -p 9696:9696 fastapi-k8s-orchestration
```

#### 5. Run with Kubernetes 

```bash
# Keep Docker running and start the Kubernetes cluster
minikube start

# Load the Docker image into minikube
minikube image load kubernetes-test-app:latest

# Deploy the Application
kubectl apply -f k8s/

# Access the Application
minikube service kubernetes-test-app

# Stop the Cluster
minikube stop
```

---

## License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT).