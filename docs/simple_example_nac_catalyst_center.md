# Step 1 - Simple Example Deployment with NaC for Catalyst Center

## Overview

In this step, you'll learn how to use Network as Code (NaC) to deploy a simple configuration to Cisco Catalyst Center.

## What is Network as Code (NaC)?

Network as Code is a framework that enables you to define, version, and deploy network infrastructure using declarative configuration files. It provides:

- **Infrastructure as Code principles** for network management
- **GitOps workflows** for network operations
- **Version control** for network configurations
- **Automated deployment** and validation

## Prerequisites

Before starting this step, ensure you have:

- Access to the lab environment
- Git repository cloned locally
- Network as Code framework installed
- Catalyst Center credentials

## Step-by-Step Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/fsalvemi/DEVWKS-1709.git
cd DEVWKS-1709
```

### 2. Review the Configuration Files

Navigate to the NaC configuration directory:

```bash
cd nac-configs
```

Examine the YAML configuration files that define the network infrastructure.

### 3. Configure Catalyst Center Connection

Edit the `config.yaml` file with your Catalyst Center details:

```yaml
catalyst_center:
  host: <your-catalyst-center-ip>
  username: <username>
  password: <password>
```

### 4. Validate the Configuration

Run validation to check your configuration:

```bash
nac validate
```

### 5. Deploy the Configuration

Deploy the configuration to Catalyst Center:

```bash
nac deploy
```

### 6. Verify the Deployment

Check the deployment status:

```bash
nac status
```

## Expected Results

After successful deployment, you should see:

- Configuration applied to Catalyst Center
- All resources created successfully
- No validation errors

## Troubleshooting

### Common Issues

**Issue**: Connection timeout to Catalyst Center
- **Solution**: Verify network connectivity and credentials

**Issue**: Validation errors
- **Solution**: Check YAML syntax and configuration values

**Issue**: Deployment fails
- **Solution**: Review logs and check resource dependencies

## Next Steps

Continue to [Step 2 (Optional) - Simple Example deployment with native Terraform](simple_example_native_terraform.md) to learn about alternative deployment methods.
