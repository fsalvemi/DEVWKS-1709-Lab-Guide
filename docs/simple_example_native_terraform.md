# Step 2 (Optional) - Simple Example Deployment with Native Terraform

## Overview

In this optional step, you'll learn how to deploy the same configuration using native Terraform without the Network as Code abstraction layer.

## What is Terraform?

Terraform is an open-source infrastructure as code software tool that provides a consistent CLI workflow to manage cloud services. Key features include:

- **Declarative configuration** using HCL (HashiCorp Configuration Language)
- **State management** for tracking infrastructure
- **Provider ecosystem** for various platforms
- **Plan and apply** workflow for safe deployments

## Prerequisites

- Terraform installed (version 1.0 or higher)
- Catalyst Center provider for Terraform
- Access to Catalyst Center API

## Step-by-Step Instructions

### 1. Navigate to Terraform Directory

```bash
cd DEVWKS-1709/terraform-configs
```

### 2. Review Terraform Configuration

Examine the `.tf` files:

```hcl
# main.tf
terraform {
  required_providers {
    catalystcenter = {
      source  = "cisco-en-programmability/catalystcenter"
      version = "~> 1.0"
    }
  }
}

provider "catalystcenter" {
  base_url = var.catalyst_center_url
  username = var.username
  password = var.password
}
```

### 3. Initialize Terraform

```bash
terraform init
```

### 4. Create Variables File

Create `terraform.tfvars`:

```hcl
catalyst_center_url = "https://<your-catalyst-center-ip>"
username = "<username>"
password = "<password>"
```

### 5. Plan the Deployment

Review what will be created:

```bash
terraform plan
```

### 6. Apply the Configuration

Deploy the infrastructure:

```bash
terraform apply
```

Type `yes` when prompted to confirm.

### 7. Verify the Deployment

Check the Terraform state:

```bash
terraform show
```

## Comparison with NaC

| Feature | Network as Code | Native Terraform |
|---------|----------------|------------------|
| Abstraction Level | High | Low |
| Configuration Format | YAML | HCL |
| Learning Curve | Easier | Steeper |
| Flexibility | Limited | Full |
| Best For | Standard deployments | Custom requirements |

## Cleanup

To remove the deployed resources:

```bash
terraform destroy
```

## Next Steps

Continue to [Step 3 (Optional) - Simple Example deployment with REST API](simple_example_rest_api.md) to learn about direct API interaction.
