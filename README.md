# 📘 AWS EKS Application Deployment with Terraform & CI/CD

## 🚀 Project Overview

This project demonstrates how to deploy a containerized web application on Amazon EKS using Docker, Kubernetes, Helm, and Jenkins CI/CD.

The solution includes:

- Docker containerization of a Flask web application
- Infrastructure provisioning using Terraform
- Kubernetes orchestration using Amazon EKS
- Container image storage in Amazon ECR
- Application deployment using Helm
- Continuous Integration and Continuous Deployment using Jenkins

As an additional implementation, a GitOps-based deployment approach using GitHub Actions and Argo CD is included in a separate `gitops` branch.

---

# ✅ Implementation Overview

| Requirement | Implementation |
|------------|----------------|
| Containerize a web application | Docker |
| Deploy application to Kubernetes | Amazon EKS |
| Infrastructure as Code | Terraform |
| Container Registry | Amazon ECR |
| Continuous Deployment Pipeline | Jenkins |
| Kubernetes Package Management | Helm |
| Auto Scaling | Horizontal Pod Autoscaler (HPA) |
| Application Exposure | AWS ALB Ingress |

---

# 🏗️ Architecture

```text
Developer
    │
    ▼
GitHub Repository
    │
    ▼
Jenkins Pipeline
    │
    ▼
Docker Build
    │
    ▼
Amazon ECR
    │
    ▼
Helm Deployment
    │
    ▼
Amazon EKS
    │
    ▼
AWS ALB Ingress
    │
    ▼
End User
```

---

# 🧰 Technologies Used

- Python (Flask)
- Docker
- Terraform
- Amazon EKS
- Kubernetes
- Helm
- Jenkins
- Amazon ECR
- AWS Load Balancer Controller (ALB)
- GitHub
- GitHub Actions (GitOps Branch)
- Argo CD (GitOps Branch)

---

# 📂 Project Structure

```text
aws-eks-devops-deployment/
│
├── app/
│   ├── app.py
│   └── Dockerfile
│
├── eks-terraform/
│   └── main.tf
│
├── helm-chart/
│   └── hello-app/
│
├── k8s/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   └── hpa.yaml
│
└── Jenkinsfile
```

---

# 📦 Application

Simple Flask application:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello, World!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

---

# 🐳 Docker

## Build Image

```bash
docker build -t hello-world-app .
```

## Run Locally

```bash
docker run -p 5000:5000 hello-world-app
```

Access:

```text
http://localhost:5000
```

Expected Output:

```text
Hello, World!
```

---

# ☁️ Infrastructure Provisioning (Terraform)

Terraform provisions:

- VPC
- Public Subnets
- Internet Gateway
- Amazon EKS Cluster
- Managed Node Group
- IAM Roles

## Commands

```bash
terraform init
terraform validate
terraform plan
terraform apply
```

---

# ☸️ Amazon EKS Deployment

## Configure kubectl

```bash
aws eks update-kubeconfig \
  --region us-east-1 \
  --name hello-eks-cluster
```

## Verify Cluster

```bash
kubectl get nodes
```

---

# 📦 Helm Deployment

Install Application:

```bash
helm install hello-app ./helm-chart/hello-app
```

Upgrade Application:

```bash
helm upgrade hello-app ./helm-chart/hello-app
```

Verify Release:

```bash
helm list
```

---

# 📊 Horizontal Pod Autoscaler (HPA)

The application automatically scales based on resource usage.

Configuration:

- CPU Utilization: 70%
- Minimum Pods: 2
- Maximum Pods: 5

Verify:

```bash
kubectl get hpa
```

---

# 🌐 Application Exposure with ALB

AWS Load Balancer Controller is used to expose the application externally.

Verify:

```bash
kubectl get ingress
```

Access:

```text
http://<ALB-DNS-NAME>
```

Expected Output:

```text
Hello, World!
```

---

# 🔄 Jenkins CI/CD Pipeline

The Jenkins pipeline automates:

1. Source Code Checkout
2. Docker Image Build
3. Amazon ECR Authentication
4. Push Docker Image to ECR
5. Update EKS kubeconfig
6. Deploy Application using Helm
7. Verify Deployment

Pipeline Flow:

```text
GitHub
   ↓
Jenkins
   ↓
Docker Build
   ↓
Amazon ECR
   ↓
Helm
   ↓
Amazon EKS
```

---

# 📦 Amazon ECR

Docker images are stored in Amazon Elastic Container Registry (ECR).

Push Image:

```bash
docker tag hello-world-app <ECR_URI>
docker push <ECR_URI>
```

---

# 🚀 Deployment Workflow

### 1. Provision Infrastructure

```bash
terraform apply
```

### 2. Configure EKS

```bash
aws eks update-kubeconfig --region us-east-1 --name hello-eks-cluster
```

### 3. Deploy Application

```bash
helm upgrade --install hello-app ./helm-chart/hello-app
```

### 4. Verify Deployment

```bash
kubectl get pods
kubectl get svc
kubectl get ingress
helm list
```

---

# ⭐ Bonus: GitOps Alternative (GitHub Actions & Argo CD)

A separate `gitops` branch demonstrates a GitOps-based deployment model.

### GitHub Actions

- Build Docker images
- Push images to Amazon ECR

### Argo CD

- Monitor Git repository
- Sync Helm charts automatically
- Deploy updates to Amazon EKS
- Self-heal configuration drift

GitOps Flow:

```text
GitHub (gitops branch)
          ↓
GitHub Actions
          ↓
Amazon ECR
          ↓
Argo CD
          ↓
Amazon EKS
```

---

# 🔐 IAM Requirements

Required AWS IAM Roles:

- EKS Cluster Role
- EKS Node Group Role
- ECR Access Permissions
- Jenkins Execution Role
- AWS Load Balancer Controller IAM Policy

---

# 🎯 Key Features Implemented

✅ Docker Containerization

✅ Infrastructure as Code (Terraform)

✅ Amazon EKS Cluster

✅ Kubernetes Deployments and Services

✅ Helm-Based Deployments

✅ Horizontal Pod Autoscaling (HPA)

✅ Amazon ECR Integration

✅ Jenkins CI/CD Pipeline

✅ AWS ALB Ingress

✅ GitOps Alternative with GitHub Actions & Argo CD

---

# 👨‍💻 Author

**Kalpana Vaddepalli**

AWS EKS & DevOps Engineering Project

Technologies: AWS • Docker • Terraform • Kubernetes • EKS • Helm • Jenkins • ECR • GitHub Actions • Argo CD

---

# 🎉 Final Outcome

This project demonstrates a complete DevOps deployment workflow using:

- Docker for containerization
- Terraform for infrastructure provisioning
- Amazon EKS for Kubernetes orchestration
- Helm for application deployment
- Jenkins for CI/CD automation
- Amazon ECR for container image storage
- AWS ALB for external access

Application Output:

```text
Hello, World!
```
