# 📘 Terraform Basics & Fundamentals

## 1. Introduction to Terraform

### ✅ What is Terraform?

Terraform is an open-source Infrastructure as Code (IaC) tool developed by HashiCorp that lets you provision and manage cloud infrastructure declaratively using HashiCorp Configuration Language (HCL).

### 🔄 Terraform vs Other IaC Tools

* **Terraform vs Ansible**: Terraform is declarative and used for provisioning; Ansible is procedural and focuses on configuration management.
* **Terraform vs CloudFormation**: CloudFormation is AWS-specific; Terraform is cloud-agnostic and supports multiple providers.

### 🧩 Terraform CLI vs Cloud vs Enterprise

* **Terraform CLI**: Local tool for running Terraform code.
* **Terraform Cloud**: Managed service for remote execution, collaboration, state management.
* **Terraform Enterprise**: Self-hosted, with advanced security, governance, and audit features.

## 2. Infrastructure as Code (IaC)

### 🛠️ What is IaC?

Managing and provisioning infrastructure using machine-readable definition files instead of manual configuration.

### 🌟 Benefits

* Version control
* Reproducibility
* Automation
* Reduced drift

## 3. Terraform Configuration Components

### 🧱 Core Blocks

* `provider`: Defines the cloud vendor.
* `resource`: Describes infrastructure components.
* `variable`: Inputs to parameterize configurations.
* `output`: Export values from modules/config.
* `data`: Fetch external data (e.g., AMI ID).
* `module`: Reusable and modular code.

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
}
```

## 4. Common Terraform Commands

* `terraform init`: Initialize working directory.
* `terraform plan`: Preview infrastructure changes.
* `terraform apply`: Apply changes.
* `terraform destroy`: Tear down resources.
* `terraform validate`: Syntax validation.
* `terraform fmt`: Format configuration files.

## 5. State Management

### 🧾 What is terraform.tfstate?

Tracks the current state of your infrastructure so Terraform knows what to create, update, or delete.

### ⚠️ Local State Risks

* Can be lost or overwritten
* Not ideal for teams (no locking)

### ☁️ Remote Backends

Use S3 + DynamoDB for shared state:

```hcl
backend "s3" {
  bucket         = "my-tf-state"
  key            = "dev/terraform.tfstate"
  region         = "us-east-1"
  dynamodb_table = "terraform-lock"
}
```

### 🔐 State Locking & Secrets

* Prevent concurrent changes using DynamoDB.
* Avoid storing sensitive data directly; mark outputs as `sensitive = true`.

## 6. Variables and Outputs

### 🔣 Variable Types

* `string`, `number`, `bool`, `list`, `map`, `object`, `tuple`

```hcl
variable "instance_count" {
  type    = number
  default = 2
}
```

### 📤 Passing Variables

* CLI: `-var="key=value"`
* `terraform.tfvars`
* Environment: `TF_VAR_key=value`

### 📥 Output Values

```hcl
output "instance_ip" {
  value = aws_instance.example.public_ip
}
```

### 🔒 Sensitive Values

```hcl
variable "db_password" {
  type      = string
  sensitive = true
}
```

## 7. Modules

### 🧩 What is a Module?

A self-contained package of Terraform configurations that manage a group of resources.

### 🚀 Benefits

* Reusability
* Better organization
* Scalability across environments

### 📦 Usage Example

```hcl
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "3.5.0"
  name    = "my-vpc"
}
```

### 📎 Module Dependencies

Use `depends_on` or output-input chaining.

## 8. Provisioning, Lifecycle, and Dependencies

### 🧷 depends\_on

```hcl
resource "aws_instance" "web" {
  depends_on = [aws_security_group.sg]
}
```

### 🔁 Lifecycle Meta-Args

```hcl
lifecycle {
  prevent_destroy      = true
  create_before_destroy = true
  ignore_changes       = [tags]
}
```

### 🔄 Provisioners

```hcl
provisioner "remote-exec" {
  inline = [
    "sudo apt update",
    "sudo apt install nginx -y"
  ]
}
```

## 9. Workspaces and Environments

### 🧮 What are Workspaces?

Multiple state files within a single config directory (e.g., dev, prod).

### 🗂️ Environment Structure

```shell
├── dev/
│   └── main.tf
├── prod/
│   └── main.tf
```

Or use:

* Variable files
* Backend key separation

## 10. Versioning & Collaboration

### 📌 Version Pinning

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}
```

### 🔒 .terraform.lock.hcl

Ensures consistent provider versions across teams.

### 🤝 Best Practices for Teams

* Remote state with locking
* Pin versions
* Use CI/CD pipelines
* Separate environments
* Always review `terraform plan`

---

