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

## 📊 Module 5: Storage and Database

(Next section content will be added here...)
