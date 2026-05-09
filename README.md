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
---
# 📦 Install AWS CLI
## Download AWS CLI
```bash 
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

sudo apt update
sudo apt install unzip -y

unzip awscliv2.zip

sudo ./aws/install

# Verify installation
aws --version

# Configure AWS credentials
aws configure
```
---

# 📦 Install Terraform

Official Documentation:

https://developer.hashicorp.com/terraform/install#linux

## Ubuntu / Debian Installation

```bash
wget -O - https://apt.releases.hashicorp.com/gpg | \
sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) \
signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com \
$(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update && sudo apt install terraform
```

## Verify Terraform

```bash
terraform version
```

---
# ☸️ Install kubectl

Official Documentation:

https://kubernetes.io/docs/tasks/tools/

## Download kubectl

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s \
https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"


## Download SHA256


curl -LO "https://dl.k8s.io/release/$(curl -L -s \
https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"


## Verify Binary


echo "$(cat kubectl.sha256) kubectl" | sha256sum --check


## Install kubectl

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

## Alternative Local Installation

```bash
chmod +x kubectl

mkdir -p ~/.local/bin

mv ./kubectl ~/.local/bin/kubectl
```

## Verify kubectl

```bash
kubectl version --client
```

---
