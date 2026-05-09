# 🎮 Super Mario Bros on AWS EKS using Terraform & Kubernetes

# 📖 Project Description

This project demonstrates the deployment of the classic **Super Mario Bros** game on a fully automated cloud-native infrastructure using **AWS EKS**, **Terraform**, **Docker**, and **Kubernetes**.

The main objective of this project is to showcase real-world **DevOps** and **Cloud Engineering** practices by automating infrastructure provisioning and application deployment in a scalable Kubernetes environment.

Using **Terraform**, the complete AWS infrastructure including:
- VPC
- Subnets
- EKS Cluster
- Worker Nodes
- Security Groups

is provisioned automatically through **Infrastructure as Code (IaC)** principles.

The application is containerized using **Docker** and deployed to the Kubernetes cluster using Kubernetes deployment and service manifests. AWS LoadBalancer service exposes the application publicly, allowing users to access and play the Super Mario Bros game directly from the browser.

---

# 🚀 Key Features

- Fully automated AWS infrastructure provisioning using Terraform
- Kubernetes cluster deployment using AWS EKS
- Docker-based containerized application deployment
- Kubernetes Deployment and Service configuration
- AWS LoadBalancer integration
- Scalable and production-style cloud infrastructure
- Infrastructure as Code (IaC) implementation
- Cloud-native application deployment workflow

---

# 🎯 Project Objectives

- Learn Kubernetes deployment on AWS
- Automate cloud infrastructure using Terraform
- Understand EKS cluster management
- Deploy containerized applications on Kubernetes
- Implement DevOps and Cloud best practices
- Gain hands-on experience with Infrastructure as Code

---

# 🚀 Project Architecture

```text
Developer
   ↓
Terraform
   ↓
AWS Infrastructure (VPC, EKS Cluster, Nodes)
   ↓
Docker Container
   ↓
Kubernetes Deployment & Service
   ↓
AWS Load Balancer
   ↓
Super Mario Bros Game 🎮
```

---

# 🛠️ Technologies Used

| Tool | Purpose |
|------|----------|
| AWS EKS | Managed Kubernetes Cluster |
| Terraform | Infrastructure as Code |
| Docker | Containerization |
| Kubernetes | Container Orchestration |
| kubectl | Kubernetes Management |
| AWS CLI | AWS Resource Management |
| Git | Version Control |

---

# 📋 Project Workflow

## Step 1 → Login & Basic Setup
- Launch AWS EC2 Instance
- Connect to EC2
- Configure IAM Role

## Step 2 → Install Required Tools
- Docker
- Terraform
- AWS CLI
- kubectl

## Step 3 → Create IAM Role
- Configure required AWS permissions

## Step 4 → Attach IAM Role to EC2
- Assign role with EKS access

## Step 5 → Build Infrastructure using Terraform
- Create EKS cluster
- Configure worker nodes
- Provision AWS resources

## Step 6 → Deploy Application on Kubernetes
- Create deployment
- Create service
- Access game using LoadBalancer URL

---

# ☁️ AWS EC2 Setup

## Launch Ubuntu EC2 Instance

Recommended:
- Instance Type: `t2.medium`
- OS: Ubuntu 22.04
- Storage: 20 GB

### Configure Security Groups

| Port | Purpose |
|------|----------|
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |
| 30000-32767 | Kubernetes NodePort |

---

# 🔐 Connect to EC2

```bash
ssh -i key.pem ubuntu@<EC2-PUBLIC-IP>
```

---

# 🐳 Step 1 — Install Docker

## Ubuntu

```bash
sudo apt update -y

sudo apt install docker.io -y

sudo systemctl start docker

sudo systemctl enable docker

sudo usermod -aG docker ubuntu

newgrp docker

docker --version
```

---

## Amazon Linux

```bash
sudo yum install docker -y

sudo systemctl start docker

sudo systemctl enable docker

sudo usermod -aG docker ec2-user

newgrp docker

docker --version
```

---

# 🏗️ Step 2 — Install Terraform

## Ubuntu

```bash
wget -O- https://apt.releases.hashicorp.com/gpg | \
sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update

sudo apt install terraform -y
```

Verify:

```bash
terraform version
```

---

## Amazon Linux

```bash
sudo yum install -y yum-utils shadow-utils

sudo yum-config-manager \
--add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo

sudo yum install terraform -y
```

---

# ☁️ Step 3 — Install AWS CLI

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" \
-o "awscliv2.zip"

sudo apt install unzip -y

unzip awscliv2.zip

sudo ./aws/install
```

Verify:

```bash
aws --version
```

---

# ☸️ Step 4 — Install kubectl

Download kubectl:

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s \
https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

Install kubectl:

```bash
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

Verify:

```bash
kubectl version --client
```

---

# 🔑 Step 5 — Configure IAM Role

## Create IAM Role

Attach:
- AdministratorAccess
- AmazonEKSClusterPolicy
- AmazonEKSWorkerNodePolicy
- AmazonEC2ContainerRegistryFullAccess

---

# 🔗 Step 6 — Attach IAM Role to EC2

Navigate:

```text
EC2 → Actions → Security → Modify IAM Role
```

Attach created IAM role to EC2 instance.

---

# ⚙️ Step 7 — Configure AWS CLI

```bash
aws configure --profile eks
```

Provide:
- AWS Access Key
- AWS Secret Key
- Region
- Output format

---

# 📂 Step 8 — Clone GitHub Repository

```bash
git clone https://github.com/CloudwithKetan/Super-Mario-Project.git
```

Navigate to project:

```bash
cd Super-Mario/EKS-TF
```

---

# 🏗️ Step 9 — Configure Terraform Backend

Edit backend configuration:

```bash
vim backend.tf
```

Update:
- Bucket name
- Region
- State file configuration

---

# 🚀 Step 10 — Build AWS Infrastructure

Initialize Terraform:

```bash
terraform init
```

Preview resources:

```bash
terraform plan
```

Create infrastructure:

```bash
terraform apply --auto-approve
```

Terraform creates:
- VPC
- Subnets
- Security Groups
- EKS Cluster
- Worker Nodes

---

# ☸️ Step 11 — Configure EKS Cluster

Update kubeconfig:

```bash
aws eks update-kubeconfig \
--name EKS_CLOUD \
--region ap-south-1 \
--profile eks
```

Verify nodes:

```bash
kubectl get nodes
```

---

# 🎮 Step 12 — Deploy Super Mario Application

Go back to root directory:

```bash
cd ..
```

---

## Create Kubernetes Deployment

```bash
kubectl apply -f deployment.yaml
```

Verify deployment:

```bash
kubectl get deployment
```

---

## Create Kubernetes Service

```bash
kubectl apply -f service.yaml
```

Verify service:

```bash
kubectl get svc
```

---

# 🌐 Step 13 — Access the Game

Get LoadBalancer URL:

```bash
kubectl get svc mario-service
```

Copy:
```text
EXTERNAL-IP
```

Open in browser:

```text
http://<LOADBALANCER-URL>
```

🎮 Enjoy Super Mario Bros!

---

# 📊 Kubernetes Verification Commands

## Check Pods

```bash
kubectl get pods
```

---

## Check Services

```bash
kubectl get svc
```

---

## Check Deployments

```bash
kubectl get deployment
```

---

## Describe Pods

```bash
kubectl describe pod <pod-name>
```

---

# 🧹 Destroy Infrastructure

Navigate to Terraform directory:

```bash
cd EKS-TF
```

Destroy infrastructure:

```bash
terraform destroy --auto-approve
```

---

# 📸 Project Screenshots

## AWS Infrastructure
```text
images/aws-eks.png
```

## Kubernetes Deployment
```text
images/kubectl-deployment.png
```

## LoadBalancer Service
```text
images/loadbalancer.png
```

## Super Mario Game Output
```text
images/final-output.png
```

---

# 🎯 Project Outcomes

✅ Infrastructure as Code using Terraform  
✅ Kubernetes Cluster Deployment on AWS  
✅ Containerized Application Deployment  
✅ Real-world DevOps Workflow  
✅ Scalable Cloud Infrastructure  
✅ Kubernetes Service Exposure using LoadBalancer  

---

# 🚀 Future Enhancements

- CI/CD Pipeline with Jenkins
- GitHub Actions Integration
- Helm Charts
- Monitoring with Prometheus & Grafana
- ArgoCD GitOps Deployment
- Auto Scaling Configuration

---

# 👨‍💻 Author

### Ketan Dhadve

DevOps Engineer | Kubernetes Enthusiast | Cloud Engineer

---

# 📚 Conclusion

This project demonstrates a complete Kubernetes deployment workflow using AWS EKS and Terraform. It highlights modern DevOps practices including Infrastructure as Code, container orchestration, cloud automation, and scalable application deployment.

The deployment of Super Mario Bros on Kubernetes provides hands-on experience with real-world cloud-native technologies and DevOps tools.

---

# ⭐ Support

If you like this project, give it a ⭐ on GitHub.
