🌐 Module 1: Introduction to Cloud

🤝 What is a Client-Server Model?

A client is an application (like a browser or desktop app) that sends requests, and a server (like an Amazon EC2 instance) responds to those requests. This architecture is the foundation of modern web computing.

☁️ Cloud Deployment Models

1️⃣ Cloud-Based Deployment

Entire application stack runs in the cloud.

Migrate legacy apps or build new ones.

Can use low-level services (like EC2) or managed services (like Lambda).

Example: An e-commerce platform hosted on EC2, RDS, and S3 within a cloud VPC.

2️⃣ On-Premises Deployment (Private Cloud)

All resources are deployed in a local data center.

Uses tools like VMware, KVM, or Hyper-V for virtualization.

Offers high control over infrastructure.

Example: Banking software running on-prem for compliance.

3️⃣ Hybrid Deployment

Combines on-premises systems with cloud services.

Useful for legacy workloads, compliance, and gradual cloud migration.

Example: Use AWS Glue and Athena for big data while keeping ERP on-prem.

✅ Summary Table

Deployment Model

Location

Use Case Example

Benefits

Cloud-Based

Cloud

SaaS, scalable applications

Scalability, flexibility

On-Premises

Local DC

Compliance-heavy legacy systems

Full control, data locality

Hybrid

Mixed

Gradual migration, hybrid analytics

Flexibility, balance

🧠 Key Takeaways

Cloud computing offers multiple deployment models tailored to business and technical needs.

The client-server model is central to how services interact over the internet.

Hybrid deployments provide a bridge between legacy systems and cloud-native applications.
