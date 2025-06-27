# ☁️ AWS: Practical Examples

This README contains a curated set of beginner-to-intermediate AWS tasks and concepts to help you learn AWS infrastructure and services with real-world analogies.

---

## 🌐 Module 1: Introduction to Cloud

### 🤝 What is a Client-Server Model?

A **client** is an application (like a browser or desktop app) that sends requests, and a **server** (like an Amazon EC2 instance) responds to those requests. This architecture is the foundation of modern web computing.

---

## ☁️ Cloud Deployment Models

### 1⃣ Cloud-Based Deployment

* Entire application stack runs in the cloud.
* Migrate legacy apps or build new ones.
* Can use low-level services (like EC2) or managed services (like Lambda).

**Example**: An e-commerce platform hosted on EC2, RDS, and S3 within a cloud VPC.

### 2⃣ On-Premises Deployment (Private Cloud)

* All resources are deployed in a local data center.
* Uses tools like VMware, KVM, or Hyper-V for virtualization.
* Offers high control over infrastructure.

**Example**: Banking software running on-prem for compliance.

### 3⃣ Hybrid Deployment

* Combines on-premises systems with cloud services.
* Useful for legacy workloads, compliance, and gradual cloud migration.

**Example**: Use AWS Glue and Athena for big data while keeping ERP on-prem.

---

## ✅ Summary Table

| Deployment Model | Location | Use Case Example                    | Benefits                    |
| ---------------- | -------- | ----------------------------------- | --------------------------- |
| Cloud-Based      | Cloud    | SaaS, scalable applications         | Scalability, flexibility    |
| On-Premises      | Local DC | Compliance-heavy legacy systems     | Full control, data locality |
| Hybrid           | Mixed    | Gradual migration, hybrid analytics | Flexibility, balance        |

---

## 🧠 Key Takeaways

* Cloud computing offers multiple deployment models tailored to business and technical needs.
* The **client-server model** is central to how services interact over the internet.
* Hybrid deployments provide a bridge between legacy systems and cloud-native applications.

---

## ⚙️ Module 2: Amazon EC2

### 💜 What is Amazon EC2?

Amazon EC2 (Elastic Compute Cloud) is a virtual server in the cloud, offering secure and resizable compute capacity.

**Benefits:**

* No upfront hardware investment
* Launch in minutes, terminate anytime
* Pay only for what you use

### 💡 EC2 Instance Types

#### General Purpose

Balanced compute, memory, and networking.

* Use cases: app servers, small DBs, game servers

#### Compute Optimized

High-performance processors.

* Use cases: high-performance web servers, batch processing

#### Memory Optimized

Designed for in-memory workloads.

* Use cases: real-time analytics, large databases

#### Accelerated Computing

Uses hardware accelerators (GPUs, FPGAs).

* Use cases: ML, graphics, pattern matching

#### Storage Optimized

Optimized for large sequential I/O.

* Use cases: data warehousing, OLTP

---

### 💰 EC2 Pricing Options

#### On-Demand

* Pay per hour/second
* Best for short-term, unpredictable workloads

#### Savings Plans

* Commit to 1–3 years
* Save up to 72%

#### Reserved Instances

* 1- or 3-year terms
* Ideal for steady-state usage

#### Spot Instances

* Use unused capacity
* Up to 90% discount, may be interrupted

#### Dedicated Hosts

* Physical servers dedicated to your use
* Best for license compliance, expensive

---

### 📈 Scaling with EC2 Auto Scaling

**Scalability:** Add/remove EC2 instances automatically.

* Helps maintain availability
* Saves costs by running only what's needed

**Approaches:**

* Dynamic Scaling: Responds to real-time demand
* Predictive Scaling: Anticipates future demand

---

### 🔄 Load Balancing with Elastic Load Balancer

**Elastic Load Balancer (ELB):**
Distributes incoming traffic across EC2 instances.

* Improves fault tolerance
* Works with Auto Scaling for optimal performance

**Coffee Shop Analogy:**

* Registers = EC2 Instances
* Barista = Load Balancer

---

### 📬 Messaging and Queuing

#### Monolithic vs Microservices

* Monolithic: Tightly coupled, one failure can bring down the app
* Microservices: Loosely coupled, resilient

#### Amazon SNS (Notification Service)

* Pub/Sub model
* Send notifications to email, Lambda, etc.

#### Amazon SQS (Queue Service)

* Message queue
* Decouples services and improves reliability

---

### 🧹 Additional Compute Services

#### AWS Lambda

* Run code without managing servers
* Triggered by events (e.g. image upload)
* Pay only when code runs

#### Containers & Orchestration

* **Amazon ECS**: Docker container orchestration
* **Amazon EKS**: Managed Kubernetes service
* **AWS Fargate**: Serverless containers for ECS/EKS

---

## 🌐 Module 3: Global Infrastructure & Reliability

### 🔠 AWS Global Infrastructure

#### 🌍 Selecting a Region

Factors to consider:

* **Compliance**: Follow legal/data regulations (e.g. GDPR)
* **Proximity**: Reduce latency by deploying closer to users
* **Available Services**: Some services are region-specific
* **Pricing**: Prices vary by region (e.g. US vs Brazil)

#### 🚧 Availability Zones (AZs)

* One or more data centers in a Region
* Low-latency but physically separate
* Ensures fault tolerance and disaster recovery

#### 🌐 Edge Locations

* Content cached close to users via Amazon CloudFront

---

### 🔧 Management Interfaces

#### AWS Management Console

* Web UI to manage AWS services
* Includes wizards, automation, and mobile app

#### AWS CLI

* Command-line access to AWS APIs
* Supports automation and scripting

#### SDKs

* Access AWS via programming languages (Java, Python, .NET, etc)
* Build apps that integrate directly with AWS

---

### 🏠 Infrastructure as Code Tools

#### AWS Elastic Beanstalk

* Deploy apps using code/configs
* Supports: load balancing, auto scaling, health monitoring

#### AWS CloudFormation

* Treat infrastructure as code
* Safely and repeatedly deploy stacks
* Rollbacks on failure

---

## 🌐 Module 4: Networking

### 🔗 Amazon VPC (Virtual Private Cloud)

* Isolated section of AWS Cloud to launch resources
* Group resources using subnets (public/private)

### 🌍 Internet Gateway & VPN Gateway

* **Internet Gateway**: Enables public access to VPC
* **Virtual Private Gateway**: Connects VPC to on-prem via VPN

### 🚪 AWS Direct Connect

* Private dedicated connection to AWS
* Bypasses public internet, increases reliability and bandwidth

---

### 📦 Subnets and Network Access Control

#### Subnets

* **Public**: Internet-facing (e.g. web servers)
* **Private**: Internal-only (e.g. databases)

#### Network ACLs

* Stateless firewall at subnet level
* Checks inbound and outbound rules independently

#### Security Groups

* Stateful firewall at EC2 instance level
* Remembers previous requests

---

### 🌐 Global Networking

#### Domain Name System (DNS)

* Translates domain names to IPs (like a phonebook)

#### Amazon Route 53

* DNS and domain registration service
* Integrates with CloudFront for CDN
* Directs users to nearest, healthy endpoints

---

# ☁️ AWS: Practical Examples

This README contains a curated set of beginner-to-intermediate AWS tasks and concepts to help you learn AWS infrastructure and services with real-world analogies.

---

## 📊 Module 5: Storage and Database

### 📂 Instance Stores

Block-level storage volumes behave like physical hard drives.
An instance store provides temporary block-level storage for an Amazon EC2 instance. An instance store is disk storage that is physically attached to the host computer for an EC2 instance, and therefore has the same lifespan as the instance. When the instance is terminated, you lose any data in the instance store.

### 📀 Amazon Elastic Block Store (Amazon EBS)

Amazon Elastic Block Store (Amazon EBS) is a service that provides block-level storage volumes that you can use with Amazon EC2 instances. If you stop or terminate an Amazon EC2 instance, all the data on the attached EBS volume remains available.

To create an EBS volume, you define the configuration (such as volume size and type) and provision it. After you create an EBS volume, it can attach to an Amazon EC2 instance.

**Amazon EBS Snapshots:**

* An EBS snapshot is an incremental backup. This means that the first backup taken of a volume copies all the data. For subsequent backups, only the blocks of data that have changed since the most recent snapshot are saved.

### 📁 Object Storage

In object storage, each object consists of:

* **Data**: Any file such as image, video, document
* **Metadata**: Info about the data (type, size, usage)
* **Key**: Unique identifier

### 💾 Amazon S3 (Simple Storage Service)

Amazon S3 stores data as **objects in buckets** and offers:

* Unlimited storage
* Max object size: 5 TB
* Versioning support

**Use Cases:**

* Website media files
* App backups
* Document archives

**Storage Classes:**

* **S3 Standard**: Frequently accessed data
* **S3 Standard-IA**: Infrequent access, lower cost
* **S3 One Zone-IA**: Infrequent access, stored in 1 AZ
* **S3 Intelligent-Tiering**: Auto moves between tiers
* **S3 Glacier Instant Retrieval**: Archive, fast access
* **S3 Glacier Flexible Retrieval**: Archive, mins to hours
* **S3 Glacier Deep Archive**: Archive, 12-48 hours
* **S3 Outposts**: Object storage on AWS Outposts (on-prem)

### 📂 Amazon EFS (Elastic File System)

* File storage solution for EC2 and on-prem
* Automatically scales up/down
* Use case: Multiple servers accessing shared files

### 📊 Amazon RDS (Relational Database Service)

* Managed relational DB service
* Automates: backups, patching, provisioning
* Supports encryption at rest and in transit

**Supported Engines:**

* Amazon Aurora
* PostgreSQL
* MySQL
* MariaDB
* Oracle
* SQL Server

**Amazon Aurora**:

* Enterprise-level
* Compatible with MySQL/PostgreSQL
* 5x faster than MySQL
* Replicates across 3 AZs

### 🔀 Amazon DynamoDB (Nonrelational)

* Key-value database
* Fast at any scale
* Ideal for applications with flexible schemas

### 📊 Amazon Redshift

* Data warehouse service
* Analyzes big data from multiple sources

### ⏫ AWS Database Migration Service (AWS DMS)

* Migrate relational and nonrelational DBs
* Source DB stays online during migration
* Supports heterogeneous migrations

### 🔎 Additional DB Services

* **Amazon DocumentDB**: Document DB for MongoDB
* **Amazon Neptune**: Graph DB for connected datasets
* **Amazon QLDB**: Ledger DB with immutable history
* **Amazon Managed Blockchain**: Build/manage blockchain networks
* **Amazon ElastiCache**: In-memory cache (Redis, Memcached)
* **DynamoDB Accelerator (DAX)**: In-memory cache for DynamoDB

---

