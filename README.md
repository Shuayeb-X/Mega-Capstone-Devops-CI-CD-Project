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

# 🚀 Install Jenkins on Jenkins VM

Official Jenkins Documentation:

https://www.jenkins.io/doc/book/installing/linux/

---

# ☕ Install Java

Jenkins requires Java to run.

## Update System Packages

```bash
sudo apt update

## Install OpenJDK 21

sudo apt install fontconfig openjdk-21-jre
```

## Verify Java Installation

```bash
java -version
```

---

# 📦 Install Jenkins

## Prerequisites

| Resource | Minimum Requirement |
|----------|---------------------|
| RAM | 256 MB |
| Storage | 1 GB |
| Recommended Storage | 10 GB (Docker Recommended) |

---

# 🔑 Add Jenkins Repository Key

```bash
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
```

---

# 📁 Add Jenkins Repository

```bash
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
https://pkg.jenkins.io/debian-stable binary/ | \
sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

---

# 📥 Install Jenkins

## Update Package Index

```bash
sudo apt update

## Install Jenkins

sudo apt install jenkins
```

---

# ✅ Verify Jenkins Service

```bash
sudo systemctl status jenkins
```

---

# 🐳 Jenkins + Docker Integration

If your goal is:

- Docker build pipelines
- CI/CD automation
- Container deployment

Then Jenkins needs Docker access.

---

# 👤 Add Jenkins User to Docker Group

```bash
sudo usermod -aG docker jenkins
```

---

# 🔄 Restart Jenkins & Docker

```bash
sudo systemctl restart jenkins
sudo systemctl restart docker
```

---

# ✅ Verify Jenkins Can Access Docker

Switch to Jenkins user:

```bash
sudo su - jenkins

Run:
```bash
docker ps
```

If Docker containers are listed successfully, Jenkins Docker integration is working correctly.

---

# 👥 Allow Both Users to Use Docker

If you want both:

- ubuntu user
- jenkins user

to access Docker:

```bash
sudo usermod -aG docker ubuntu
sudo usermod -aG docker jenkins
```

---

# 🔐 Install Trivy

Trivy is used for:

- Vulnerability scanning
- Sensitive data detection
- Security analysis
- Hardcoded secret scanning

---

# 📦 Install Required Packages

```bash
sudo apt-get install wget gnupg
```

---

# 🔑 Add Trivy GPG Key

```bash
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
```

---

# 📁 Add Trivy Repository

```bash
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] \
https://aquasecurity.github.io/trivy-repo/deb generic main" | \
sudo tee -a /etc/apt/sources.list.d/trivy.list
```

---

# 📥 Install Trivy

## Update Package Index

```bash
sudo apt-get update
## Install Trivy
sudo apt-get install trivy
```

---

# ✅ Verify Trivy Installation

```bash
trivy --version
```

---

# 📌 Useful Commands

## Check Jenkins Status

```bash
sudo systemctl status jenkins

## Restart Jenkins

sudo systemctl restart jenkins

## Check Docker Status

```bash
sudo systemctl status docker
```

## Verify Docker Access

```bash
docker ps
```

## Verify Trivy

```bash
trivy --version
```

---

# 🔍 Install SonarQube on SonarQube VM

SonarQube is used for:

- Bug Detection
- Syntax Error Analysis
- Code Quality Analysis
- Security Vulnerability Detection
- Code Smell Detection
- Report Generation

---

# 📦 Update System Packages

```bash
sudo apt update
```

---

# 🐳 Install Docker

Make sure Docker is installed before running SonarQube.

## Verify Docker Installation

```bash
docker --version
```

---

# 🚀 Run SonarQube using Docker

```bash
docker run -d \
  --name sonar \
  -p 8080:9000 \
  sonarqube:lts-community
```

---

# ✅ Verify SonarQube Container

```bash
docker ps
```

You should see:

```text
sonarqube:lts-community
```

running on:

```text
8080:9000
```

---

# 🌐 Access SonarQube Dashboard

Open browser:

```text
http://<YOUR_VM_IP>:8080
```

Example:

```text
http://192.168.1.10:8080
```

---

# 🔑 Default SonarQube Credentials

| Username | Password |
|----------|----------|
| admin | admin |

---

# 📊 SonarQube Features

SonarQube can analyze:

- Java
- Spring Boot
- Python
- JavaScript
- Node.js
- Go
- Kubernetes YAML
- Terraform
- Dockerfiles

---

# 📌 Common SonarQube Commands

## Check Running Containers

```bash
docker ps
```

## View SonarQube Logs

```bash
docker logs sonar
```

## Restart SonarQube

```bash
docker restart sonar
```

## Stop SonarQube

```bash
docker stop sonar
```

---

# 📦 Install Nexus Repository on Nexus VM

Nexus Repository Manager is used for:

- Docker Image Storage
- Maven Artifact Storage
- CI/CD Artifact Management
- Private Repository Hosting

---

# 📦 Update Packages

```bash
sudo apt update
```

---

# 🚀 Run Nexus Container

```bash
docker run -d \
  --name nexus \
  -p 9090:8081 \
  sonatype/nexus3
```

---

# ✅ Verify Nexus Container

```bash
docker ps
```

You should see:

```text
sonatype/nexus3
```

running on:

```text
9090:8081
```

---

# 🌐 Access Nexus Dashboard

Open browser:

```text
http://<YOUR_VM_IP>:9090
```

Example:

```text
http://192.168.1.10:9090
```

---

# 🔑 Nexus Default Credentials

## Default Username

```text
admin
```

---

# 🔐 Get Initial Admin Password

```bash
docker exec nexus cat /nexus-data/admin.password
```

Copy the generated password and login to Nexus.

---

# 📌 Common Nexus Commands

## Check Running Containers

```bash
docker ps
```

## View Nexus Logs

```bash
docker logs nexus
```

## Restart Nexus

```bash
docker restart nexus
```

## Stop Nexus

```bash
docker stop nexus
```

---




