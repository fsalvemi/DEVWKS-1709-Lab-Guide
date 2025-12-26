# Overview

This is a demonstration repository for **DEVWKS-1709 Lab** and includes four repositories that cover two scenarios and three learning objectives

| Scenario | Repository | Approach | Learning Objective | 
|----------|--------------|---------|---------|
| Simple Example| nac-catalystcenter-simple-example | Network as Code for Catalyst Center | Familiarize with Network as Code for Catalyst Center |
| Simple Example| native-terraform-simple-example | Native Terraform | Comparing approach complexity |
| Simple Example| native-api-simple-example | Native Catalyst Center API | Comparing approach complexity |
| Comprehensive Example | nac-catalystcenter-comprehensive-example | Network as Code for Catalyst Center | Demonstrate full SDA Fabric Deployment |

The first three repositories demonstrates three approaches to achieve the **identical outcome**: deploying a complete site hierarchy with IP pools and reservations to Cisco Catalyst Center.

The first example allows to familiarize with the Network as Code for Catalyst Center solution.
The second and third examples try to achieve the same result using Native Terraform and Native Catalyst Center API. This allows to compare the complexity, maintainability, and ease of use of the three approaches.

The forth repository includes comprehensive example that deploys a full SD-Access fabric using the Network as Code for Catalyst Center approach.
This demonstrates how Network as Code for Catalyst Center can be used to deploy a full SD-Access fabric

# Suggested Learning Path

- Access the Lab in dCloud

Follow the instructions for [Lab Access](./lab_access.md)

- Step 1: Use the Simple Example deployment scenario to familiarize with Network as Code for Catalyst Center

Follow the lab guide for the [nac-catalystcenter approach](./simple_example_nac_catalyst_center.md)

- Step 2 (Optional): Try to achieve the same results using the Terraform Native API approach

Follow the lab guide for the [Terraform Native API approach](./simple_example_native_terraform.md) and compare the complexity of the code required to achieve the same result

- Step 3 (Optional): Try to achieve the same results using the Catalyst Center Native API approach

Examine the complexity of the [native API example](./simple_example_rest_api.md) and compare the complexity of the code required to achieve the same result

- Step 4: Review Approach Comparison

Review the [Approach Comparison](./review_approach_comparison.md) to understand the complexity differences between the three approaches used in the Simple Example scenario.

- Step 5 (Stretch): Deploy a complete SD-Access Fabric

Follow the lab guide for the [nac-catalystcenter-comprehensive-example](./deploy_complete_sd_access_fabric.md)
