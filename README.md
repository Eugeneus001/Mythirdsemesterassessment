# Retail App Cloud Infrastructure

## About This Project
This project sets up the cloud infrastructure for the **Retail Store Application** using **AWS**, **Terraform**, and **EKS**. The goal is to create a scalable, secure, and automated environment to run a microservices-based retail app.

This work is part of my **Third Semester Assessment 2** for Cloud DevOps Engineering.

---

## How It’s Built

Here’s a quick overview of the infrastructure:

- **VPC** – A custom Virtual Private Cloud with public subnets and an Internet Gateway for connectivity.  
- **EKS Cluster** – A managed Kubernetes cluster for running the microservices.  
- **Node Group** – EC2 instances (t2.medium) connected to the cluster to run workloads.  
- **Terraform Backend** –  
  - S3 bucket: "yusuf-project-bedrock-tfstate" 
  - DynamoDB table: "yusuf-project-bedrock-locks" (used for state locking)  
- **IAM Users & Roles** –  
  - Developer user with read-only access to the cluster  
  - Node IAM role for worker nodes  
  - Cluster IAM role for managing the EKS control plane  

## Getting Started

Ready to launch your cloud environment? Follow these simple steps:

1. **Set Up Your Workspace**  
   Make sure you have your AWS credentials configured, and that Terraform and kubectl are installed.

2. **Initialize Terraform**  
terraform init

3. **Deploy the Infrastructure
terraform apply
Confirm the plan with yes. it creates the VPC, EKS cluster, node group, S3 bucket, DynamoDB table, and IAM roles/users.

4. **Connection to The Cluster
"aws eks update-kubeconfig --region eu-west-2 --name staging-altsch_project"
Checking The Cluster

"kubectl get nodes"
"kubectl get pods"


#Terraform Backend#
The remote backend stores Terraform state safely in S3 and uses DynamoDB for state locking:

terraform {
  backend "s3" {
    bucket         = "yusuf-project-bedrock-tfstate"
    key            = "infra/terraform.tfstate"
    region         = "eu-west-3"
    dynamodb_table = "yusuf-project-bedrock-locks"
  }
}
