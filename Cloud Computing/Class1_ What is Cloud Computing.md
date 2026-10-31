# Cloud Computing – Complete Notes

## 1. What is Cloud Computing?

Cloud computing is the delivery of computing resources, such as servers, storage, databases, networking and software, over the internet on an on-demand basis.

**In simple words:** Instead of purchasing and maintaining physical servers, users can rent computing resources from cloud providers and access them through the internet.

**Examples:**
- Amazon Web Services (AWS)
- Microsoft Azure
- Google Cloud Platform (GCP)

**Real-world example:** If you deploy a Node.js application on AWS EC2, you rent a virtual server instead of purchasing and maintaining a physical server.

---

## 2. Characteristics of Cloud Computing

There are five essential characteristics of cloud computing:

### 1. On-demand Self-service
Users can access computing resources whenever they need them without requiring direct assistance from the service provider.

### 2. Broad Network Access
Cloud services are accessible over the internet through devices such as laptops, smartphones and tablets.

### 3. Resource Pooling
Cloud providers share computing resources among multiple customers using a multi-tenant architecture.

### 4. Rapid Elasticity
Computing resources can be scaled up or down quickly according to workload requirements.

### 5. Measured Service
Resource usage is monitored, measured and billed according to consumption (pay-as-you-go).

---

## 3. Benefits of Cloud Computing

| Benefit | Explanation |
|---|---|
| Cost Efficiency | Reduces upfront hardware and infrastructure costs. |
| Scalability | Easily increases or decreases computing resources. |
| Flexibility | Provides access to resources from different locations. |
| High Availability | Helps maintain services with minimal downtime. |
| Disaster Recovery | Supports data backup and recovery. |
| Security | Provides security tools, encryption and access control. |
| Automatic Updates | Providers maintain and update underlying infrastructure. |
| Performance | Offers access to powerful computing resources. |
| Global Accessibility | Allows applications to serve users across different regions. |

---

## 4. Types of Cloud Computing

Cloud computing is generally classified into two major categories:

1. Cloud Service Models
2. Cloud Deployment Models

### A. Cloud Service Models

There are three fundamental cloud service models:

#### 1. IaaS – Infrastructure as a Service

IaaS provides virtualised computing resources, such as servers, storage, networking and virtual machines.

**You manage:**
- Operating system
- Runtime
- Applications
- Data

**Provider manages:**
- Physical servers
- Networking
- Virtualisation

**Examples:**
- AWS EC2
- Google Compute Engine
- Azure Virtual Machines

**Real-world example:** You rent an AWS EC2 instance, install Ubuntu, configure Node.js and deploy your application.

#### 2. PaaS – Platform as a Service

PaaS provides a ready-to-use environment for developing, testing and deploying applications without managing the underlying infrastructure.

**You manage:**
- Application code
- Data

**Provider manages:**
- Infrastructure
- Operating system
- Runtime
- Middleware

**Examples:**
- Heroku
- Google App Engine
- Azure App Service

**Real-world example:** You push your Node.js application to Heroku, and the platform manages the underlying server and runtime environment.

#### 3. SaaS – Software as a Service

SaaS provides ready-made software applications accessible through a web browser or application.

**You manage:**
- Your account
- Application settings
- Your data usage

**Provider manages:**
- Application
- Runtime
- Operating system
- Infrastructure

**Examples:**
- Gmail
- Google Docs
- Microsoft 365

**Real-world example:** You use Gmail to send and receive emails without managing its servers or infrastructure.

### Service Model Comparison

| Responsibility | IaaS | PaaS | SaaS |
|---|---|---|---|
| Application | You | You | Provider |
| Data | You | You | Shared / provider-managed |
| Runtime | You | Provider | Provider |
| Operating System | You | Provider | Provider |
| Virtualisation | Provider | Provider | Provider |
| Servers | Provider | Provider | Provider |
| Networking | Provider | Provider | Provider |

**Easy way to remember:**
- IaaS = Rent the infrastructure.
- PaaS = Rent the development platform.
- SaaS = Use the finished software.

---

### B. Cloud Deployment Models

A cloud deployment model describes where cloud infrastructure is hosted, who owns it, who manages it and who can access it.

There are four primary cloud deployment models:

#### 1. Public Cloud

A public cloud is a cloud environment where infrastructure is owned and operated by a third-party provider and delivered to customers over the internet.

**Characteristics:**
- Infrastructure is shared among multiple customers.
- Usually follows a pay-as-you-go pricing model.
- Highly scalable and flexible.
- The provider manages the underlying infrastructure.

**Examples:**
- Amazon Web Services (AWS)
- Microsoft Azure
- Google Cloud Platform (GCP)

**Real-world example:** A company deploys its website on AWS instead of purchasing and maintaining physical servers.

#### 2. Private Cloud

A private cloud is a cloud environment dedicated to a single organisation. It can be hosted within the organisation's own data centre or by a third-party provider.

**Characteristics:**
- Dedicated to one organisation.
- Greater control over infrastructure and security configurations.
- Supports customisation.
- Usually requires more management and maintenance.

**Examples:**
- OpenStack
- VMware Cloud Foundation

**Real-world example:** A bank maintains its own private cloud to host sensitive financial systems and customer information.

#### 3. Hybrid Cloud

A hybrid cloud combines private cloud infrastructure with public cloud services, allowing data and applications to move between the two environments.

**Characteristics:**
- Combines public and private cloud environments.
- Provides flexibility in workload distribution.
- Sensitive data can remain in a private environment.
- Public cloud resources can handle additional workloads.

**Real-world example:** A bank stores sensitive customer information in its private cloud but uses AWS public cloud resources to handle additional traffic.

#### 4. Community Cloud

A community cloud is shared by several organisations that have similar requirements, such as security, compliance or operational objectives.

**Characteristics:**
- Shared by multiple organisations.
- Organisations have common requirements.
- Infrastructure and costs can be shared.
- Access is restricted to participating organisations.

**Real-world example:** Several government departments share cloud infrastructure to manage government services and sensitive information.

### Deployment Model Comparison

| Feature | Public | Private | Hybrid | Community |
|---|---|---|---|---|
| Ownership | Provider | Single organisation | Mixed | Shared |
| Infrastructure | Shared | Dedicated | Combined | Shared |
| Cost | Usually lower initial cost | Usually higher | Varies | Shared |
| Scalability | High | Depends on capacity | High | Depends on capacity |
| Control | Limited | High | Mixed | Shared governance |
| Security control | Shared responsibility | Greater organisational control | Mixed | Shared requirements |

---

## 5. Service Models vs Deployment Models

These are two different classifications.

| Service Models | Deployment Models |
|---|---|
| IaaS | Public Cloud |
| PaaS | Private Cloud |
| SaaS | Hybrid Cloud |
| | Community Cloud |

**Service models describe WHAT services the cloud provides.**

**Deployment models describe HOW and WHERE cloud infrastructure is deployed.**

For example, AWS EC2 is an IaaS service that can be used in a public cloud deployment.

---

## 6. Interview Quick Revision

### What is Cloud Computing?

Cloud computing is the on-demand delivery of computing resources over the internet, allowing users to access scalable infrastructure and services without owning or managing physical hardware.

### What are the five characteristics of cloud computing?

1. On-demand self-service
2. Broad network access
3. Resource pooling
4. Rapid elasticity
5. Measured service

### What are the three cloud service models?

1. IaaS – Infrastructure as a Service
2. PaaS – Platform as a Service
3. SaaS – Software as a Service

### What are the four cloud deployment models?

1. Public Cloud
2. Private Cloud
3. Hybrid Cloud
4. Community Cloud

### Why do organisations use cloud computing?

Organisations use cloud computing to reduce infrastructure costs, improve scalability, increase availability, simplify maintenance and access computing resources globally.

---

## 7. Important Cloud Computing Vocabulary

| Term | Meaning |
|---|---|
| Scalability | Ability to increase or decrease resources to handle workload changes. |
| Elasticity | Ability to automatically or dynamically adjust resources based on demand. |
| Virtualisation | Creating virtual versions of computing resources. |
| Multi-tenancy | Multiple customers sharing the same underlying infrastructure. |
| Availability | The ability of a system to remain accessible and operational. |
| Reliability | The ability of a system to perform consistently over time. |
| Pay-as-you-go | Paying only for the resources consumed. |
| Infrastructure | The underlying hardware and networking resources. |
| Workload | The amount of processing or tasks handled by a system. |
| Disaster Recovery | Processes for restoring systems and data after a failure. |

---

## 8. Learning Roadmap: What to Study Next

After understanding cloud computing fundamentals, follow this learning sequence:

1. AWS Fundamentals
2. AWS Global Infrastructure (Regions and Availability Zones)
3. EC2 – Elastic Compute Cloud
4. S3 – Simple Storage Service
5. IAM – Identity and Access Management
6. VPC – Virtual Private Cloud
7. Load Balancing and Auto Scaling
8. RDS – Relational Database Service
9. Docker and Containerisation
10. Kubernetes and Container Orchestration
11. CI/CD and Cloud Deployment
12. Cloud Security and Monitoring

**Final takeaway:**

- Characteristics = How cloud computing works.
- Benefits = Why organisations use cloud computing.
- Service models = What services cloud providers offer.
- Deployment models = How and where cloud infrastructure is deployed.
