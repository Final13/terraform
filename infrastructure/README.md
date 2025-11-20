# Infrastructure as Code

Terraform configuration for AWS infrastructure deployment.

## Structure

```
infrastructure/
└── terraform/
    ├── main.tf              # Main Terraform configuration
    ├── variables.tf         # Variable definitions
    ├── outputs.tf           # Output values
    ├── vpc.tf               # VPC configuration
    ├── eks.tf               # EKS cluster configuration
    ├── ecr.tf               # ECR repository configuration
    ├── bootstrap.sh         # Bootstrap script for S3 backend
    └── terraform.tfvars.example  # Example variables file
```

## Prerequisites

- Terraform >= 1.5.0
- AWS CLI configured with appropriate credentials
- kubectl (for EKS cluster management)

## Setup

1. **Bootstrap Terraform Backend** (first time only):
   ```bash
   cd terraform
   chmod +x bootstrap.sh
   ./bootstrap.sh
   ```
   This creates an S3 bucket for Terraform state and DynamoDB table for state locking.

2. **Update main.tf** with the bucket name from bootstrap output.

3. **Configure variables**:
   ```bash
   cp terraform.tfvars.example terraform.tfvars
   # Edit terraform.tfvars with your values
   ```

4. **Initialize Terraform**:
   ```bash
   cd terraform
   terraform init
   ```

5. **Plan and Apply**:
   ```bash
   terraform plan
   terraform apply
   ```

## Resources Created

- VPC with public and private subnets
- EKS cluster
- ECR repository
- Node groups for EKS

## Variables

See `terraform/variables.tf` for all available variables. Copy `terraform.tfvars.example` to `terraform.tfvars` and customize as needed.

## State Management

Terraform state is stored in S3 with DynamoDB locking. The backend configuration is in `terraform/main.tf`.

