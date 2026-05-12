# Terraform Workflow Documentation

This document records the step-by-step execution of Terraform commands and observations made during the lab.

## 1. `terraform init`
- **What it does:** Downloads the AWS provider plugin and initializes the `.terraform` directory.
- **Observation:** Terraform created a `.terraform.lock.hcl` file to manage provider versions.

## 2. `terraform fmt` & `terraform validate`
- **What it does:** `fmt` rewrites configuration files to a canonical format. `validate` checks the configuration for internal consistency.
- **Observation:** Even if the code looks "okay," `fmt` often fixes small alignment issues.

## 3. `terraform plan`
- **What it does:** Generates an execution plan. It compares the current state with the desired state in the `.tf` files.
- **Typical Output:** `Plan: 2 to add, 0 to change, 0 to destroy.`

## 4. `terraform apply`
- **What it does:** Executes the actions proposed in the plan.
- **Observation:** This command prompted for a `yes` confirmation before calling AWS APIs to create the S3 bucket.

## 5. `terraform output`
- **What it does:** Reads and prints the values defined in `output` blocks from the state file.
- **Benefit:** Allows easy access to the Bucket ARN and Name without checking the AWS Console.

## 6. Observations about the State File (`terraform.tfstate`)
- The state file is stored in **JSON format**.
- It contains sensitive metadata including resource IDs, ARNs, and full configuration attributes.
- **Crucial Note:** I verified that `.tfstate` is included in `.gitignore` to prevent it from being pushed to the public repository, as it contains the "digital twin" of my infrastructure.

## 7. `terraform destroy`
- **What it does:** Terminates all resources managed by the local configuration.
- **Observation:** Terraform effectively used the state file to identify exactly what to delete, ensuring no "zombie" resources were left behind in AWS.