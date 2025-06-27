# ☁️ Terraform on AWS: Practical Examples

This README contains a curated set of beginner-to-intermediate Terraform tasks to help you learn AWS infrastructure provisioning using Terraform.

---

## 1. 🚀 EC2 Instance

### Objective

Provision an EC2 instance with a key pair and tag.

### Concepts

* AWS Provider
* EC2 resource
* Key Pair, Tags

```hcl
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  key_name      = "my-key-pair"

  tags = {
    Name = "ExampleInstance"
  }
}

output "instance_public_ip" {
  value = aws_instance.example.public_ip
}
```

---

## 2. 🌐 VPC and Subnets

### Objective

Create a custom VPC with two public subnets.

### Concepts

* CIDR Blocks
* Availability Zones

```hcl
resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"
}

resource "aws_subnet" "subnet1" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.1.0/24"
  availability_zone = "us-west-2a"
}

resource "aws_subnet" "subnet2" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.2.0/24"
  availability_zone = "us-west-2b"
}

output "vpc_id" {
  value = aws_vpc.main.id
}
```

---

## 3. 🪣 S3 Bucket

### Objective

Create an S3 bucket with versioning.

### Concepts

* Versioning

```hcl
resource "aws_s3_bucket" "example" {
  bucket = "my-unique-bucket-name-123"

  versioning {
    enabled = true
  }
}

output "bucket_name" {
  value = aws_s3_bucket.example.bucket
}
```

---

## 4. 🔐 Security Group

### Objective

Allow only SSH traffic.

### Concepts

* Ingress/Egress Rules

```hcl
resource "aws_security_group" "example" {
  name        = "example-sg"
  description = "Allow SSH access"

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

output "security_group_id" {
  value = aws_security_group.example.id
}
```

---

## 5. 📦 Module Usage

### Objective

Use a custom module to deploy EC2.

### Concepts

* Reusability

**Module (modules/ec2/main.tf)**

```hcl
resource "aws_instance" "example" {
  ami           = var.ami
  instance_type = var.instance_type
}

variable "ami" {}
variable "instance_type" {}

output "instance_public_ip" {
  value = aws_instance.example.public_ip
}
```

**Main (main.tf)**

```hcl
module "ec2_instance" {
  source        = "./modules/ec2"
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}

output "instance_public_ip" {
  value = module.ec2_instance.instance_public_ip
}
```

---

## 6. 🗃️ Remote State Backend

### Objective

Configure Terraform state on S3.

### Concepts

* State Management, Locking

```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state-bucket"
    key            = "terraform.tfstate"
    region         = "us-west-2"
    encrypt        = true
    dynamodb_table = "terraform-lock-table"
  }
}
```

---

## 7. 🔐 IAM Role & Policy

### Objective

Allow EC2 to access S3.

### Concepts

* IAM Roles, Policies, Attachments

```hcl
resource "aws_iam_role" "ec2_role" {
  name = "ec2-role"
  assume_role_policy = jsonencode({
    Version = "2012-10-17",
    Statement = [{
      Action = "sts:AssumeRole",
      Principal = { Service = "ec2.amazonaws.com" },
      Effect = "Allow",
      Sid = ""
    }]
  })
}

resource "aws_iam_policy" "s3_access" {
  name        = "EC2S3Access"
  description = "Allow EC2 access to S3"
  policy      = jsonencode({
    Version = "2012-10-17",
    Statement = [{
      Action = "s3:*",
      Effect = "Allow",
      Resource = "arn:aws:s3:::my-bucket/*"
    }]
  })
}

resource "aws_iam_role_policy_attachment" "ec2_s3_policy" {
  policy_arn = aws_iam_policy.s3_access.arn
  role       = aws_iam_role.ec2_role.name
}
```

---

## 8. 🧪 RDS Instance

### Objective

Create a PostgreSQL database on RDS.

### Concepts

* RDS Instance, Credentials, Storage

```hcl
resource "aws_db_instance" "example" {
  identifier         = "example-db"
  engine             = "postgres"
  username           = "dbuser"
  password           = "dbpassword"
  instance_class     = "db.t2.micro"
  allocated_storage  = 20
}

output "db_endpoint" {
  value = aws_db_instance.example.endpoint
}
```

---

## 9. 📈 Auto Scaling Group

### Objective

Create an Auto Scaling Group.

### Concepts

* Launch Configuration, Desired Capacity

```hcl
resource "aws_launch_configuration" "example" {
  name          = "example-launch-config"
  image_id      = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}

resource "aws_autoscaling_group" "example" {
  desired_capacity     = 1
  max_size             = 3
  min_size             = 1
  vpc_zone_identifier  = ["subnet-12345678"]
  launch_configuration = aws_launch_configuration.example.id
}
```

---

## 10. ⚖️ Application Load Balancer (ALB)

### Objective

Distribute traffic across EC2 instances.

### Concepts

* ALB, Listener, Target Group

```hcl
resource "aws_lb" "example" {
  name               = "example-alb"
  internal           = false
  load_balancer_type = "application"
  security_groups    = ["sg-12345678"]
  subnets            = ["subnet-12345678", "subnet-23456789"]
  enable_deletion_protection = false
}

resource "aws_lb_target_group" "example" {
  name     = "example-targets"
  port     = 80
  protocol = "HTTP"
  vpc_id   = "vpc-12345678"
}

resource "aws_lb_listener" "example" {
  load_balancer_arn = aws_lb.example.arn
  port              = 80
  protocol          = "HTTP"
  default_action {
    type             = "forward"
    target_group_arn = aws_lb_target_group.example.arn
  }
}
```

---

## ✅ Summary: Key Concepts

* Providers: `provider "aws" {}`
* Resources: EC2, VPC, Subnet, IAM, RDS, S3, ALB
* Outputs & Variables
* Modules: DRY and reusable code
* State Management: Remote backends, locking
* Networking, Security, Scaling, Load Balancing
