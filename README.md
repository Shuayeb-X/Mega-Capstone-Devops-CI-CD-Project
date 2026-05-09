# Mega-Capstone-Devops-CI-CD-Project
# 🚀 Complete DevOps CI/CD Pipeline using AWS EKS, Terraform, Jenkins, Kubernetes, SonarQube, Trivy & Monitoring

A complete production-style DevOps project using:

- AWS EKS
- Terraform
- Jenkins
- Docker
- Kubernetes
- SonarQube
- Trivy
- Nexus
- NGINX Ingress
- AWS EBS CSI Driver
- Prometheus
- Grafana

---

# 📌 Project Architecture

```text
GitHub Repo
     |
     v
Jenkins CI Pipeline
     |
     |---- Build Application
     |---- SonarQube Analysis
     |---- Trivy Security Scan
     |---- Docker Build & Push
     |
     v
Jenkins CD Pipeline
     |
     v
Kubernetes Manifests
     |
     v
Amazon EKS Cluster
     |
     |---- Deployment
     |---- Service
     |---- PVC/PV
     |---- HPA
     |---- Ingress
     |
     v
Monitoring Stack
     |
     |---- Prometheus
     |---- Grafana
```

---

# 🛠️ Tech Stack

| Tool | Purpose |
|------|----------|
| AWS EKS | Kubernetes Cluster |
| Terraform | Infrastructure as Code |
| Jenkins | CI/CD Automation |
| Docker | Containerization |
| Kubernetes | Container Orchestration |
| SonarQube | Code Quality Analysis |
| Trivy | Vulnerability Scanning |
| Nexus | Artifact Repository |
| NGINX Ingress | Routing Traffic |
| EBS CSI Driver | Persistent Storage |
| Prometheus | Monitoring |
| Grafana | Visualization |
