# 🚀 Three-Tier DevSecOps CI/CD Project

This project demonstrates how to build and deploy a **three-tier web application** (Frontend, Backend, and Database) using a **DevSecOps pipeline** on AWS.  
It integrates **CI/CD**, **security scanning**, **monitoring**, and **GitOps** for production-ready delivery.

---

## 🗂️ Table of Contents
- [Project Overview]
- [Architecture]
- [Tech Stack]
- [Pipeline Workflow])
- [Key Features]
- [Prerequisites]
- [Setup Instructions]
- [Repository Structure]
- [Monitoring & Security]
- [Future Improvements]

---

## 📌 Project Overview
The goal is to showcase a **real-world enterprise DevSecOps workflow** where code flows through:

1. **Version Control** → GitHub  
2. **Continuous Integration** → Jenkins (Build → Test → Scan)  
3. **Continuous Delivery** → AWS ECR → Kubernetes (EKS)  
4. **Security** → SonarQube, OWASP Dependency-Check, Trivy  
5. **Monitoring** → Prometheus + Grafana  
6. **GitOps** → ArgoCD for automatic deployments

✅ The pipeline enforces **code quality, vulnerability scanning, container scanning, and automated deployments**.

---

## 🏗️ Architecture

### 🔹 Workflow Overview:
- **Frontend:** React App  
- **Backend:** Python Flask API  
- **Database:** AWS RDS (MySQL)  
- **CI/CD:** Jenkins Declarative Pipeline automating Build → Scan → Deploy  
- **Security:** SonarQube, OWASP Dependency-Check, Trivy  
- **Monitoring:** Prometheus & Grafana on Kubernetes  
- **GitOps:** ArgoCD to sync Kubernetes manifests from GitHub  
- **Cloud Services:** AWS EKS, ECR, IAM, Load Balancers, RDS, S3  

---

## 🛠️ Tech Stack

| Category              | Tool / Service                         |
|-----------------------|----------------------------------------|
| **Version Control**   | GitHub                                  |
| **CI/CD**             | Jenkins                                 |
| **Containerization**  | Docker                                  |
| **Container Registry**| AWS ECR                                 |
| **Orchestration**     | Kubernetes (Amazon EKS)                 |
| **Security Scans**    | SonarQube, OWASP Dependency-Check, Trivy|
| **Monitoring**        | Prometheus, Grafana                     |
| **Database**          | AWS RDS (MySQL)                         |
| **GitOps**            | ArgoCD                                  |
| **Infrastructure**    | Terraform *(optional)*                  |

---

## 🔄 Pipeline Workflow

1. **Code pushed to GitHub**
2. **Jenkins Pipeline Stages:**
   - 🧹 Clean Workspace  
   - 📥 Checkout Code  
   - 🔎 SonarQube Code Analysis  
   - 🛡️ OWASP Dependency-Check  
   - 🐳 Docker Build & Tag  
   - 📦 Push Image to AWS ECR  
   - 🔍 Trivy Image Scan  
   - 📜 Update Kubernetes Manifests  
   - 🚀 Deploy to EKS via ArgoCD
3. **Prometheus & Grafana** monitor health and performance.
4. **Quality Gates** block the pipeline on critical vulnerabilities.

---

## ⭐ Key Features
- ⚡ **End-to-End CI/CD** with Jenkins  
- 🔐 **Integrated Security** at every stage  
- 🔄 **GitOps Deployment** using ArgoCD  
- 📊 **Centralized Monitoring** with Prometheus & Grafana  
- ☁️ **AWS Cloud-Native** setup with scalability in mind  

---

## 📋 Prerequisites
- AWS Account with:
  - EKS cluster & worker nodes
  - RDS MySQL database
  - IAM roles for Jenkins/EKS/ECR
- Jenkins server on EC2
- SonarQube & OWASP installed
- `kubectl`, `aws` CLI configured locally
- Docker installed locally
- Optional: Terraform for infrastructure provisioning

---

## ⚙️ Setup Instructions

### 1️⃣ Clone the Repository

git clone https://github.com/marioaaziz/three-tier-devsecops-project.git
cd three-tier-devsecops-project

2️⃣ Configure AWS

Create EKS cluster

Configure kubectl to connect to EKS

Setup RDS MySQL for backend

Create ECR repository for Docker images

3️⃣ Setup Jenkins

Install plugins:

Git, Docker, SonarQube, Dependency-Check, Trivy

Add Credentials:

AWS keys, ECR repo name, GitHub credentials

Create a new pipeline job using the included Jenkinsfile

4️⃣ Install Monitoring Stack
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack -n monitoring --create-namespace

5️⃣ Deploy ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.4.7/manifests/install.yaml
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

6️⃣ Run the Pipeline

Trigger build from Jenkins or via webhook

Monitor progress in Jenkins → Console Output

Verify deployment using the LoadBalancer URL of the service.

📂 Repository Structure
three-tier-devsecops-project/
├── app-code/
│   ├── frontend/            # React frontend
│   ├── backend/             # Flask backend
│   └── Dockerfile
├── k8s-manifests/           # Kubernetes YAML files
├── scripts/                 # Helper scripts
├── Jenkinsfile              # CI/CD pipeline
├── README.md
└── architecture.png

📈 Monitoring & Security

Grafana Dashboards: for Kubernetes and app performance

Prometheus: for metrics and alerting

SonarQube: enforces code quality gates

Trivy: scans containers & files for vulnerabilities

OWASP Dependency-Check: scans app dependencies for CVEs

🔮 Future Improvements

Automate all AWS infrastructure with Terraform

Add Slack/MS Teams notifications to pipeline

Secure Grafana & ArgoCD with HTTPS

Add Canary deployments using Argo Rollouts

📷 Screenshots

(Add screenshots after running your pipeline)

✅ Jenkins pipeline stages

✅ SonarQube code quality dashboard

✅ Trivy vulnerability scan results

✅ Grafana metrics dashboard

✅ ArgoCD GitOps sync view
