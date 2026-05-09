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

# 🚀 Create EKS Terraform Cluster

Terraform project:

```text
Eks_Terraform
```

---

# 🔐 Configure IAM OIDC Provider

The IAM OIDC provider is required for:

- Connecting Amazon EKS with AWS IAM
- Enabling IAM Roles for Service Accounts (IRSA)

---

# 📌 Relationship

```text
OIDC Provider  ---> REQUIRED FIRST

IAM Service Account ---> Uses OIDC
```

---

# ✅ Correct Order

```text
1. Create OIDC Provider First ✅

2. Create IAM Service Account ✅
```

---

# 📦 Create IAM Service Account for EBS CSI Driver

Run:

```bash
eksctl create iamserviceaccount \
  --region ap-south-1 \
  --name ebs-csi-controller-sa \
  --namespace kube-system \
  --cluster test-cluster \
  --attach-policy-arn arn:aws:iam::aws:policy/service-role/AmazonEBSCSIDriverPolicy \
  --approve \
  --override-existing-serviceaccounts
```

---

# 🚀 Apply Terraform Again

After creating the IAM service account:

```bash
terraform apply -auto-approve
```

---

# 🔗 Configure kubectl

Connect kubectl with AWS EKS cluster:

```bash
aws eks --region ap-south-1 update-kubeconfig --name test-cluster
```

This command allows:

- kubectl
- Amazon EKS

to communicate with each other.

---

# 💾 Install AWS EBS CSI Driver

Run:

```bash
kubectl apply -k \
"github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/ecr/?ref=release-1.11"
```

The EBS CSI Driver enables:

- Dynamic Persistent Volumes
- EBS Storage Integration
- PVC Support in Kubernetes

---

# 🌐 Install NGINX Ingress Controller

Run:

```bash
kubectl apply -f \
https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
```

---

# ✅ Verify Cluster Nodes

Check nodes:

```bash
kubectl get nodes
```

Expected output:

```text
STATUS   Ready
```

---

# ⚠️ IMPORTANT NOTES

Do NOT add:

- OIDC Terraform resource
- EBS Addon initially

---

# 📌 Recommended Approach

First make sure:

- EKS Cluster works
- Node Group works
- kubectl connects successfully

Only after that:

- Add EBS CSI Driver
- Configure advanced addons

---

# 📦 Check System Pods

Run:

```bash
kubectl get pods -A
```

You should see:

- kube-system pods
- ingress-nginx pods
- aws-node pods
- coredns pods

running successfully.

---

# ✅ Infrastructure Created

After successful setup, your infrastructure includes:

| Component | Status |
|-----------|--------|
| VPC | ✅ |
| Subnets | ✅ |
| EKS Cluster | ✅ |
| Node Group | ✅ |
| kubectl Connected | ✅ |
| OIDC Provider | ✅ |

---

# 📌 Useful Commands

## Check Cluster Nodes

```bash
kubectl get nodes
```

---

## Check All Pods

```bash
kubectl get pods -A
```

---

## Check kube-system Pods

```bash
kubectl get pods -n kube-system
```

---

## Verify kubectl Context

```bash
kubectl config current-context
```

---

## Verify EKS Cluster

```bash
aws eks list-clusters
```

---

# 🏆 Best Practices

- Create OIDC before IAM Service Accounts
- Verify cluster before installing addons
- Use EBS CSI for dynamic storage
- Use Terraform for infrastructure automation
- Keep Terraform state secure

---

---

# 📦 Kubernetes Manifest Includes

Manifest includes:

- Namespace
- Secret
- EBS StorageClass
- PVC
- Deployment
- Service
- HPA
- Ingress

using AWS EBS dynamic storage provisioning in Kubernetes.

---

# ⚠️ Important Note

Don't create a manual PersistentVolume (PV) because with:

- AWS EBS CSI
- StorageClass

Kubernetes creates the PV automatically.

---

# 🚀 Dynamic Provisioning

This is called:

```text
Dynamic Provisioning
```

---

# 📌 Flow

```text
PVC ---> StorageClass ---> AWS EBS Volume ---> PV auto-created
```

---

# 📦 When PVC is Created

So when this PVC is created:

```yaml
kind: PersistentVolumeClaim
```

Kubernetes automatically:

- creates AWS EBS disk
- creates PersistentVolume
- binds PV to PVC

---

# ✅ Verify PersistentVolume

Run:

```bash
kubectl get pv
```

You will see an automatically created PV.

# 🔐 RBAC Permission

## 1. ServiceAccount

```yaml
apiVersion: v1
kind: ServiceAccount

metadata:
  name: jenkins
  namespace: webapps
```

---

## 2. Role

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role

metadata:
  name: jenkins-role
  namespace: webapps

rules:

  # Permissions for core API resources
  - apiGroups: [""]
    resources:
      - secrets
      - configmaps
      - persistentvolumeclaims
      - services
      - pods
    verbs:
      - get
      - list
      - watch
      - create
      - update
      - delete
      - patch

  # Permissions for apps API group
  - apiGroups: ["apps"]
    resources:
      - deployments
      - replicasets
      - statefulsets
    verbs:
      - get
      - list
      - watch
      - create
      - update
      - delete
      - patch

  # Permissions for networking API group
  - apiGroups: ["networking.k8s.io"]
    resources:
      - ingresses
    verbs:
      - get
      - list
      - watch
      - create
      - update
      - delete
      - patch

  # Permissions for autoscaling API group
  - apiGroups: ["autoscaling"]
    resources:
      - horizontalpodautoscalers
    verbs:
      - get
      - list
      - watch
      - create
      - update
      - delete
      - patch
```

---

## 3. RoleBinding

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding

metadata:
  name: jenkins-rolebinding
  namespace: webapps

roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: jenkins-role

subjects:
  - kind: ServiceAccount
    name: jenkins
    namespace: webapps
```

---

## 4. ClusterRole

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole

metadata:
  name: jenkins-cluster-role

rules:

  # Permissions for persistentvolumes
  - apiGroups: [""]
    resources:
      - persistentvolumes
    verbs:
      - get
      - list
      - watch
      - create
      - update
      - delete

  # Permissions for storageclasses
  - apiGroups: ["storage.k8s.io"]
    resources:
      - storageclasses
    verbs:
      - get
      - list
      - watch
      - create
      - update
      - delete

  # Permissions for ClusterIssuer
  - apiGroups: ["cert-manager.io"]
    resources:
      - clusterissuers
    verbs:
      - get
      - list
      - watch
      - create
      - update
      - delete
```

---

## 5. ClusterRoleBinding

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding

metadata:
  name: jenkins-cluster-rolebinding

roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: jenkins-cluster-role

subjects:
  - kind: ServiceAccount
    name: jenkins
    namespace: webapps
```

---

# 🚀 Apply All RBAC Files

```bash
kubectl apply -f serviceaccount.yaml

kubectl apply -f role.yaml

kubectl apply -f rolebinding.yaml

kubectl apply -f clusterrole.yaml

kubectl apply -f clusterrolebinding.yaml
```

---

# ✅ Verify ServiceAccount Permissions

```bash
kubectl auth can-i create secrets \
--as=system:serviceaccount:webapps:jenkins -n webapps
```

```bash
kubectl auth can-i create storageclasses \
--as=system:serviceaccount:webapps:jenkins
```

```bash
kubectl auth can-i create persistentvolumes \
--as=system:serviceaccount:webapps:jenkins
```

---

# 🔑 Token for Jenkins Deployment Permission

```yaml
apiVersion: v1
kind: Secret

type: kubernetes.io/service-account-token

metadata:
  name: mysecretname

  annotations:
    kubernetes.io/service-account.name: myserviceaccount
```

---

# 📌 Verify Jenkins Secret

```bash
kubectl describe secret jenkins-secret -n webapps
```

---

# 📦 Important Note

Create the RBAC file inside your:

```text
CD Repository
```

because the CD pipeline deploys Kubernetes manifests.

---

# 🚀 Repository Setup

```text
CI Repo  ---> Builds Docker Image

CD Repo  ---> Deploys Kubernetes Manifests
```

---

# 📄 Create RBAC File

Create:

```text
jenkins-rbac.yaml
```

inside your:

```text
CD Repository
```

# 🔐 Jenkins Kubernetes RBAC Permission

Jenkins Kubernetes service account exists

But it does NOT have permission to manage:

- ingress
- deployments
- services
- pvc etc.

---

# ✅ You Need

- Role
- RoleBinding

---

# 📄 Create `jenkins-rbac.yaml`

```yaml
apiVersion: v1
kind: ServiceAccount

metadata:
  name: jenkins
  namespace: webapps

---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role

metadata:
  namespace: webapps
  name: jenkins-role

rules:

- apiGroups: [""]
  resources:
    - pods
    - services
    - secrets
    - configmaps
    - persistentvolumeclaims
  verbs:
    - get
    - list
    - watch
    - create
    - update
    - patch
    - delete

- apiGroups: ["apps"]
  resources:
    - deployments
    - replicasets
  verbs:
    - get
    - list
    - watch
    - create
    - update
    - patch
    - delete

- apiGroups: ["networking.k8s.io"]
  resources:
    - ingresses
  verbs:
    - get
    - list
    - watch
    - create
    - update
    - patch
    - delete

- apiGroups: ["autoscaling"]
  resources:
    - horizontalpodautoscalers
  verbs:
    - get
    - list
    - watch
    - create
    - update
    - patch
    - delete

- apiGroups: ["storage.k8s.io"]
  resources:
    - storageclasses
  verbs:
    - get
    - list
    - watch
    - create
    - update
    - patch
    - delete

---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding

metadata:
  name: jenkins-rolebinding
  namespace: webapps

subjects:
- kind: ServiceAccount
  name: jenkins
  namespace: webapps

roleRef:
  kind: Role
  name: jenkins-role
  apiGroup: rbac.authorization.k8s.io
```

---

# 🚀 Apply RBAC File

Run:

```bash
kubectl apply -f jenkins-rbac.yaml
```

---

# 🔄 Rerun Jenkins Pipeline

Now rerun:

```text
Jenkins CD Pipeline
```

---

# ✅ Pipeline Can Now Deploy

Your pipeline should successfully apply:

- ingress
- deployment
- service
- pvc
- hpa
- secret

inside namespace:

```text
webapps
```

using:

```text
Jenkins Kubernetes RBAC permissions
```

---

# 🚀 Run CD Jenkins Pipeline

Now run your:

```text
CD Jenkins Pipeline
```

# 🌐 Fix NGINX Ingress Controller Issues

Sometimes ingress does not work.

In that case follow these steps:

---

# ✅ 1. Check Ingress Controller

Run:

```bash
kubectl get pods -n ingress-nginx
```

---

# 🔄 2. Reinstall Ingress Controller

If pods are:

- missing
- not running

then reinstall ingress controller.

Run:

```bash
kubectl apply -f \
https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
```

---

# ⏳ 3. Wait 2–3 Minutes

Wait for ingress controller pods to start.

---

# 📊 4. Install Metrics Server (Optional but Recommended)

Metrics server is required for:

- HPA
- CPU monitoring
- autoscaling
- Kubernetes metrics

Run:

```bash
kubectl apply -f \
https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

---

# ✅ Verify Metrics Server

Run:

```bash
kubectl get deployment metrics-server -n kube-system
```

---

# 🔍 Check Ingress Pods Again

Run:

```bash
kubectl get pods -n ingress-nginx
```

You should see:

```text
Running
```

---

# ⚠️ IMPORTANT

Edit your GitHub file:

```text
Manifest/manifest.yaml
```

---

# 🚨 If Ingress Pods Are Stuck in Pending

Example:

```text
Pending
```

That means:

```text
Kubernetes cannot schedule pods on your node
```

---

# 📌 Most Common Reason

Your EKS node:

```text
t3.micro
```

does NOT have enough:

- CPU
- Memory

---

# 📦 Installed Components

You installed:

- ingress-nginx
- cert-manager
- EBS CSI
- MySQL
- HPA

but your cluster only has:

```text
1 x t3.micro
```

which is too small.

---

# 🔍 Check Exact Error

Run:

```bash
kubectl describe pod ingress-nginx-controller-7d65c586d6-4t62j -n ingress-nginx
```

At the bottom you will likely see:

```text
Insufficient cpu
```

or

```text
Insufficient memory
```

---

# ✅ Best Fix

Increase node instance type.

---

# 📄 Edit Terraform `main.tf`

Change:

```hcl
instance_types = ["t3.micro"]
```

to:

```hcl
instance_types = ["t3.small"]
```

or preferably:

```hcl
instance_types = ["t3.medium"]
```

---

# 📈 Increase Node Count

Update:

```hcl
desired_size = 2

max_size = 2

min_size = 1
```

---

# 🚀 Apply Terraform Changes

Run:

```bash
terraform apply -auto-approve
```

Terraform will update the node group.

---

# ✅ Verify Nodes

After a few minutes run:

```bash
kubectl get nodes
```

You should see:

```text
2 nodes
```

---

# 🔍 Verify Ingress Pods

Run:

```bash
kubectl get pods -n ingress-nginx
```

Pods should become:

```text
Running
```

---

# 🔄 Rerun Jenkins Pipeline

Now rerun:

```text
Jenkins CD Pipeline
```

---

# 🎯 Final Result

Your ingress creation should finally succeed.

---

# ✅ Expected Working Components

- ingress-nginx
- metrics-server
- HPA
- EBS CSI
- cert-manager
- MySQL
- Jenkins CD pipeline

all running successfully inside your EKS cluster.

# 🔐 Create ClusterIssuer using cert-manager

## `cluster-issuer.yaml`

```yaml
apiVersion: cert-manager.io/v1
kind: ClusterIssuer

metadata:
  name: letsencrypt-prod

spec:
  acme:
    server: https://acme-v02.api.letsencrypt.org/directory

    email: office@devopsshack.com

    privateKeySecretRef:
      name: letsencrypt-prod

    solvers:
      - http01:
          ingress:
            class: nginx
```

---

# 🚀 Apply ClusterIssuer

Run:

```bash
kubectl apply -f cluster-issuer.yaml
```

---

# ✅ Verify ClusterIssuer

Run:

```bash
kubectl get clusterissuer
```

You should see:

```text
letsencrypt-prod   True
```

---

# 📌 Purpose

This creates a:

```text
cert-manager ClusterIssuer
```

using:

- Let’s Encrypt
- NGINX Ingress

---

# 🌐 Use Simpler Ingress

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress

metadata:
  name: mysql-ingress
  namespace: webapps

  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /

spec:
  ingressClassName: nginx

  rules:
    - http:
        paths:
          - path: /
            pathType: Prefix

            backend:
              service:
                name: mysql-service

                port:
                  number: 3306
```

---

# 🚀 Apply Manifest

Run:

```bash
kubectl apply -f Manifest/manifest.yaml
```

---

# 🔄 Run Jenkins Pipeline Again

Now rerun:

```text
Jenkins CD Pipeline
```

---

# ✅ Verify Deployment from EKS/DevOps VM

## Check All Resources

```bash
kubectl get all -n webapps
```

---

# 🌐 Check Ingress

```bash
kubectl get ingress -n webapps
```

---

# 💾 Check PVC

```bash
kubectl get pvc -n webapps
```

---

# 📦 Check PV

```bash
kubectl get pv
```

---

# 🎯 Expected Result

You should see:

- mysql pod running
- ingress created
- pvc bound
- pv bound
- load balancer address available

---

# ✅ Full CI/CD + EKS Flow Working

Now your full deployment flow is working successfully with:

- Jenkins
- Kubernetes
- Amazon EKS
- NGINX Ingress Controller
- Amazon EBS CSI Driver


# ☕ Fix Spring Boot Application Configuration

## Spring Boot App Configuration

In your BankApp source code:

Open:

```text
src/main/resources/application.properties
```

---

# 🔧 Replace Datasource Settings

Replace existing datasource configuration with:

```properties
spring.datasource.url=jdbc:mysql://${DB_HOST}:${DB_PORT}/${DB_NAME}

spring.datasource.username=${DB_USER}

spring.datasource.password=${DB_PASSWORD}

spring.jpa.hibernate.ddl-auto=update

spring.jpa.show-sql=true

spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
```

---

# 🚀 Rerun Jenkins CD Pipeline

After updating:

```text
application.properties
```

rerun:

```text
Jenkins CD Pipeline
```

---

# ✅ Verify Pods

Run:

```bash
kubectl get pods -n webapps
```

You want:

```text
Running
```

for:

- bankapp
- mysql

---

# 🌐 Access Application

Now you can access your application using:

```text
http://a1d2492cf9b394405b60ec60c5fdc9d8-1364725057.ap-south-1.elb.amazonaws.com
```

---

# 🏆 Better Practice

## For MySQL

Keep MySQL service as:

```text
ClusterIP
```

Do NOT create ingress for MySQL.

---

# 🌐 For Your Actual Website/Application

Create ingress only for:

- frontend
- backend app
- APIs

---

# 📌 Recommended Flow

```text
Frontend App ---> Ingress ---> Service ---> Pods
                                  |
                                  ---> MySQL Service
```

---

# 💾 Best Practice for Databases

Use:

- StatefulSet
- PVC
- Secret

instead of:

- plain Deployment
- hardcoded credentials

---

# ✅ Recommended Kubernetes Database Setup

```text
StatefulSet + PVC + Secret
```

---

# 🎯 Final Result

After configuration:

✅ Spring Boot Connected to MySQL  
✅ Kubernetes Secrets Used  
✅ Jenkins CD Pipeline Working  
✅ Application Running on EKS  
✅ MySQL Running with Persistent Storage  
✅ Ingress Working Successfully


# 📊 Monitoring Setup using Prometheus & Grafana

## Create `values.yaml`

```yaml
alertmanager:
  enabled: false

prometheus:
  prometheusSpec:
    storageSpec:
      volumeClaimTemplate:
        spec:
          storageClassName: ebs-sc

          accessModes:
            - ReadWriteOnce

          resources:
            requests:
              storage: 5Gi

  service:
    type: LoadBalancer

grafana:
  enabled: true

  adminUser: admin
  adminPassword: admin123

  service:
    type: LoadBalancer

nodeExporter:
  enabled: true

kubeStateMetrics:
  enabled: true

additionalScrapeConfigs:

  - job_name: node-exporter

    static_configs:
      - targets:
          - monitoring-prometheus-node-exporter:9100

  - job_name: kube-state-metrics

    static_configs:
      - targets:
          - monitoring-kube-state-metrics:8080
```

---

# 🚀 Add Prometheus Helm Repository

Run:

```bash
helm repo add prometheus-community \
https://prometheus-community.github.io/helm-charts
```

---

# 🔄 Update Helm Repository

Run:

```bash
helm repo update
```

---

# 📦 Install Monitoring Stack

Run:

```bash
helm upgrade --install monitoring \
prometheus-community/kube-prometheus-stack \
-f values.yaml \
-n monitoring \
--create-namespace
```

---

# ✅ Check Monitoring Pods

Run:

```bash
kubectl get pods -n monitoring
```

Wait until all pods become:

```text
Running
```

---

# 🌐 Get Monitoring Services

Run:

```bash
kubectl get svc -n monitoring
```

You will get external:

- Grafana LoadBalancer URL
- Prometheus LoadBalancer URL

---

# 🌍 Enable External IP

Run:

```bash
kubectl patch svc monitoring-kube-prometheus-prometheus \
-n monitoring \
-p '{"spec":{"type":"LoadBalancer"}}'
```

---

```bash
kubectl patch svc monitoring-kube-state-metrics \
-n monitoring \
-p '{"spec":{"type":"LoadBalancer"}}'
```

---

```bash
kubectl patch svc monitoring-prometheus-node-exporter \
-n monitoring \
-p '{"spec":{"type":"LoadBalancer"}}'
```

---

# ✅ Verify External IP

Run:

```bash
kubectl get svc -n monitoring
```

You should see:

```text
EXTERNAL-IP
```

---

# 📊 Monitoring Components Enabled

- Prometheus
- Grafana
- Node Exporter
- kube-state-metrics

---

# 📈 Features Included

## Prometheus

- Metrics collection
- Kubernetes monitoring
- Alerting support

---

## Grafana

- Dashboards
- Visualization
- Monitoring UI

Default credentials:

```text
Username: admin
Password: admin123
```

---

## Node Exporter

Provides:

- CPU metrics
- Memory metrics
- Disk metrics
- Node metrics

---

## kube-state-metrics

Provides:

- Pod metrics
- Deployment metrics
- StatefulSet metrics
- Cluster object metrics

---

# 🎯 Final Result

Your full DevOps stack is now running:

✅ Terraform  
✅ AWS EKS  
✅ Jenkins CI/CD  
✅ DockerHub image deployment  
✅ Kubernetes manifests  
✅ Ingress + LoadBalancer  
✅ Persistent storage (EBS/PVC/PV)  
✅ MySQL database  
✅ Spring Boot BankApp  
✅ Prometheus monitoring  
✅ Grafana dashboards  
✅ Node Exporter metrics  
✅ kube-state-metrics  

---

# 🚀 Complete Production-Style Environment

This is now a complete:

```text
Production-style DevOps/Kubernetes Environment
```

using:

- AWS EKS
- Terraform
- Jenkins
- Kubernetes
- Prometheus
- Grafana
- EBS Storage
- CI/CD Pipeline
- Monitoring Stack


