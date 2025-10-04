Three-Tier DevSecOps CI/CD Project

This project demonstrates how to build and deploy a three-tier web application (frontend, backend, and database) using a DevSecOps pipeline on AWS.
It integrates modern CI/CD practices, security scanning, monitoring, and GitOps for production-ready delivery.

🗂️ Table of Contents

Project Overview

Architecture

Tech Stack

Pipeline Workflow

Key Features

Prerequisites

Step-by-Step Setup

Repository Structure

Monitoring & Security

Future Improvements



📌 Project Overview

The goal of this project is to simulate real-world enterprise delivery pipelines where code goes through:

Version control → GitHub

Continuous Integration → Jenkins (build, lint, test, security scans)

Continuous Delivery/Deployment → AWS ECR + Kubernetes (EKS)

Security → SonarQube, OWASP Dependency-Check, Trivy

Monitoring → Prometheus, Grafana

GitOps → ArgoCD for Kubernetes deployments

✅ This project showcases how DevOps and Security can be integrated seamlessly into every stage of application delivery.

🏗️ Architecture

The architecture includes:

Frontend: React-based static UI

Backend: Python Flask API

Database: AWS RDS (MySQL)

CI/CD: Jenkins pipeline automating code build → scan → containerize → deploy

Security Tools: SonarQube, OWASP Dependency-Check, Trivy image/file scans

Monitoring: Prometheus + Grafana for app metrics and dashboards

GitOps: ArgoCD to keep Kubernetes manifests in sync with GitHub

AWS Services: EKS, ECR, IAM, Load Balancers, RDS, S3 for storage

🛠️ Tech Stack
Category	Tool / Service
Version Control	GitHub
CI/CD	Jenkins (Declarative Pipeline)
Containerization	Docker
Container Registry	AWS ECR
Orchestration	Kubernetes (Amazon EKS)
Monitoring	Prometheus, Grafana
Security	SonarQube, OWASP Dependency-Check, Trivy
Database	AWS RDS (MySQL)
IaC (optional)	Terraform for AWS infra
GitOps	ArgoCD
Cloud	AWS
🔄 Pipeline Workflow

Developer pushes code → GitHub triggers Jenkins build

Jenkins stages:

Clean workspace

Checkout code

SonarQube analysis (code quality & vulnerabilities)

OWASP Dependency-Check (library vulnerabilities)

Trivy file scan

Docker build & tag

Push Docker image → AWS ECR

Trivy image scan

Update Kubernetes manifests (deployment YAML)

ArgoCD sync → deploy to EKS

Monitoring & Alerts with Prometheus + Grafana

Quality Gates fail the pipeline if critical vulnerabilities are found.

⭐ Key Features

End-to-End CI/CD: Automated builds and deployments

Built-in Security Scans: Code, dependencies, container images

GitOps with ArgoCD: Ensures cluster state matches GitHub repo

Centralized Monitoring: Application metrics and dashboards

Scalable Cloud Architecture: AWS EKS & Load Balancers

Production-like Workflow: Reflects how DevSecOps works in real enterprises

📋 Prerequisites

AWS Account with:

EKS cluster + worker nodes

IAM roles for Jenkins, ECR, and ArgoCD

Jenkins server (EC2 instance)

SonarQube & OWASP Dependency-Check installed on Jenkins

kubectl & aws CLI configured locally

Docker installed locally for testing

Optional: Terraform scripts for infra provisioning

⚙️ Step-by-Step Setup
1. Clone Repo
git clone https://github.com/marioaaziz/three-tier-devsecops-project.git
cd three-tier-devsecops-project

2. Setup AWS Resources

Create an EKS cluster and worker nodes

Configure kubectl context to point to EKS

Create an RDS MySQL database for the backend

Configure AWS CLI with proper credentials

3. Jenkins Configuration

Install required plugins:

Git, Docker, SonarQube Scanner, OWASP Dependency-Check, Kubernetes CLI, Trivy

Add credentials in Manage Jenkins → Credentials:

AWS_ACCOUNT_ID, AWS_ECR_REPO_NAME

GitHub credentials

SonarQube token

Create a Declarative Pipeline Job

Point it to the Jenkinsfile in this repo

4. Deploy Monitoring Stack
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack -n monitoring --create-namespace

5. Deploy ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.4.7/manifests/install.yaml
kubectl patch svc argocd-server -n argocd -p '{"spec":{"type":"LoadBalancer"}}'

6. Run the Pipeline

Trigger the Jenkins build manually or via GitHub webhook

Monitor logs in Jenkins → Console Output

Verify deployed application on EKS via LoadBalancer URL

📂 Repository Structure
├── app-code/
│   ├── frontend/          # React frontend
│   ├── backend/           # Flask backend
│   └── Dockerfile
├── k8s-manifests/         # Kubernetes YAML files
├── Jenkinsfile            # CI/CD pipeline script
├── scripts/               # Helper scripts
├── README.md
└── architecture.png

📈 Monitoring & Security

Grafana Dashboards: Import community dashboards for Kubernetes and application metrics

Prometheus: Monitors pod health, CPU, memory, etc.

SonarQube: Enforces code quality gates

Trivy: Scans files and container images for CVEs

OWASP Dependency-Check: Scans libraries for known vulnerabilities

🚀 Future Improvements

Implement Terraform fully for infrastructure as code

Add automated Slack/MS Teams notifications for pipeline events

Enable HTTPS for Grafana and ArgoCD

Introduce Canary Deployments with Argo Rollouts
