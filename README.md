# -AWS-EKS-Infrastructure---Terraform-GitOps
![Terraform](https://img.shields.io/badge/terraform-v1.6+-blue) ![AWS](https://img.shields.io/badge/AWS-EKS-orange) ![GitOps](https://img.shields.io/badge/GitOps-enabled-green)

## Overview

Production-ready Terraform infrastructure repository implementing GitOps principles for AWS EKS cluster provisioning. This repository manages VPC networking, EKS clusters, security groups, and IAM roles through automated CI/CD pipelines.

## Architecture

This infrastructure follows a **two-branch strategy**:
- **Staging Branch**: Validates Terraform changes without applying to production
- **Main Branch**: Applies approved changes to production AWS infrastructure

### Key Components

- **VPC Module**: Multi-AZ networking with public/private subnets, NAT gateways, Internet gateways
- **EKS Module**: Managed Kubernetes cluster with auto-scaling node groups
- **Security**: IAM roles, security groups, and RBAC configurations
- **State Management**: Remote state storage in S3 with DynamoDB locking

## Prerequisites

- Terraform >= 1.6
- AWS CLI configured with appropriate credentials
- GitHub account with repository access
- IAM permissions for VPC, EKS, EC2, and IAM resources

- ## Workflow

### Staging Branch Workflow
1. Create feature branch from `staging`
2. Modify Terraform code
3. Push changes to trigger validation workflow
4. Review `terraform plan` output in GitHub Actions
5. Create Pull Request to merge into `main`

### Main Branch Workflow
1. PR approval required from designated reviewers
2. Merge triggers `terraform apply` automatically
3. Infrastructure changes applied to AWS
4. State file updated in S3 backend


## Monitoring

Monitor infrastructure state through:
- **AWS Console**: Real-time resource visualization
- **Terraform State**: Version-controlled infrastructure tracking
- **GitHub Actions Logs**: Pipeline execution history

## Security Best Practices

- Remote state encryption enabled in S3
- State file locking with DynamoDB
- IAM roles with least privilege principles
- Security groups with minimal required access
- Secrets stored in GitHub Secrets (never committed)
- Branch protection rules enforced on main

