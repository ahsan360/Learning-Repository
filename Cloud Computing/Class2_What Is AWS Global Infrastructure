# AWS Global Infrastructure

## 1. What Is AWS Global Infrastructure?

AWS Global Infrastructure is the worldwide network of data centres and related infrastructure that Amazon Web Services (AWS) uses to deliver cloud services.

It enables businesses to deploy applications globally, improve availability, reduce latency and scale their infrastructure.

### Benefits
- **Low latency:** Deploy applications closer to users.
- **High availability:** Distribute workloads across multiple locations.
- **Scalability:** Increase or decrease computing resources according to demand.
- **Fault tolerance:** Reduce the impact of infrastructure failures.
- **Global reach:** Deliver applications and services to users worldwide.
- **Disaster recovery:** Support recovery using infrastructure in other locations.

---

## 2. Main Components of AWS Global Infrastructure

The key components are:

1. Regions
2. Availability Zones (AZs)
3. Data Centres
4. Edge Locations
5. Local Zones
6. AWS Wavelength Zones

---

## 3. AWS Regions

### Definition

An AWS Region is a separate geographical area where AWS operates its cloud infrastructure.

Each Region contains multiple Availability Zones.

### Examples

| Region | Region Code | Location |
|---|---|---|
| US East (N. Virginia) | `us-east-1` | United States |
| Europe (Frankfurt) | `eu-central-1` | Germany |
| Asia Pacific (Mumbai) | `ap-south-1` | India |
| Asia Pacific (Singapore) | `ap-southeast-1` | Singapore |

*Note: These are examples, not a complete list of AWS Regions.*

### Why Are Regions Important?

- Reduce latency by placing resources closer to users.
- Help meet data residency and regulatory requirements.
- Provide access to AWS services available in a particular Region.
- Support disaster recovery strategies.
- Allow organisations to choose infrastructure locations based on cost and performance.

### Example

If most of your users are in Germany, you might deploy your application in the Frankfurt Region.

### Important Point

Resources in one Region are not automatically replicated to another Region in every case. Cross-Region replication must be configured when required.

---

## 4. Availability Zones (AZs)

### Definition

An Availability Zone is an isolated location within an AWS Region. Each AZ consists of one or more data centres.

Availability Zones within a Region are connected through high-bandwidth, low-latency networking.

### Example

```text
AWS Region: Frankfurt (eu-central-1)
|
|--- Availability Zone A
|      |--- Data Centre(s)
|
|--- Availability Zone B
|      |--- Data Centre(s)
|
|--- Availability Zone C
       |--- Data Centre(s)
```

This is a conceptual diagram, not a representation of the exact physical layout of a Region.

### Why Are Availability Zones Important?

- Improve application availability.
- Reduce dependence on a single location.
- Support fault-tolerant architectures.
- Allow workloads to be distributed across separate locations.
- Help applications continue operating during certain infrastructure failures.

### Example

Suppose you deploy two EC2 instances:

- Instance 1 in AZ-A
- Instance 2 in AZ-B

If AZ-A experiences a failure, the application may continue serving users through AZ-B, provided the remaining infrastructure has sufficient capacity and is configured appropriately.

### Important Point

Deploying resources across multiple AZs does not automatically guarantee high availability. Load balancing, data replication, failover and other dependencies must also be configured correctly.

---

## 5. Data Centres

### Definition

A data centre is a physical facility that houses computing equipment, including servers, storage systems and networking devices.

### Main Components

- Physical servers
- Storage systems
- Networking equipment
- Power supplies and backup power
- Cooling systems
- Physical security systems

### Example

When you launch an Amazon EC2 instance, AWS manages the underlying physical infrastructure on which your virtual machine runs.

### Important Point

An Availability Zone may contain multiple data centres. An AZ is not necessarily a single building.

---

## 6. Edge Locations

### Definition

An Edge Location is a site within AWS's edge network that helps deliver content and services closer to end users.

Edge Locations are particularly important for Amazon CloudFront, a content delivery network (CDN).

### Benefits

- Reduce content delivery latency.
- Cache frequently requested content closer to users.
- Reduce repeated requests to the origin server.
- Improve website performance for geographically distributed users.

### Example

Suppose your website's origin server is in Germany and a user accesses it from Bangladesh.

CloudFront may cache static files at an Edge Location closer to the user.

```text
User in Bangladesh
        |
        v
Nearby Edge Location
        |
        | Cache miss
        v
Origin Server in Germany
```

If the requested content is already cached and valid, CloudFront can serve it directly from the edge.

### Important Point

An Edge Location is not the same as an Availability Zone.

- Regions provide core cloud infrastructure.
- Edge Locations help deliver content closer to users.

---

## 7. AWS Local Zones

### Definition

An AWS Local Zone extends selected AWS infrastructure closer to a particular metropolitan area.

It allows supported computing and other resources to run closer to users who require low latency.

### Benefits

- Reduce latency for selected workloads.
- Support latency-sensitive applications.
- Bring computing resources closer to specific population centres.

### Example

A company developing a real-time gaming application might use a suitable Local Zone to run supported workloads closer to players in a particular city.

### Important Point

Local Zones are available only in selected locations and support particular AWS services.

---

## 8. AWS Wavelength Zones

### Definition

AWS Wavelength brings selected AWS computing and storage services into telecommunications providers' 5G networks.

It supports applications that require very low latency for mobile and connected devices.

### Benefits

- Reduce latency for certain mobile applications.
- Support real-time processing near 5G-connected devices.
- Enable selected edge computing use cases.

### Example

A developer builds a real-time application for connected devices using a supported 5G network. AWS Wavelength may allow the application to process data closer to those devices.

### Important Point

Wavelength Zones are designed for specific edge computing use cases involving telecommunications networks.

---

## 9. Comparison of Infrastructure Components

| Component | Meaning | Main Purpose |
|---|---|---|
| Region | Separate geographical area | Choose the general deployment location |
| Availability Zone | Isolated location within a Region | Improve availability and resilience |
| Data Centre | Physical facility containing computing equipment | Provide physical computing infrastructure |
| Edge Location | Site in AWS's edge network | Deliver content closer to users |
| Local Zone | Selected infrastructure near a metropolitan area | Support latency-sensitive workloads |
| Wavelength Zone | Selected AWS services within 5G networks | Support low-latency mobile applications |

---

## 10. Region vs Availability Zone

| Feature | Region | Availability Zone |
|---|---|---|
| Meaning | Separate geographical area | Isolated location within a Region |
| Structure | Contains multiple AZs | Contains one or more data centres |
| Main purpose | Select infrastructure location | Distribute workloads within a Region |
| Example | `eu-central-1` | `eu-central-1a` |
| Disaster recovery | Can support cross-Region recovery | Can support multi-AZ resilience |

### Important Note About AZ Names

AWS Availability Zone letter names, such as `us-east-1a`, may refer to different physical zones in different AWS accounts.

Availability Zone IDs provide consistent identifiers for the underlying physical locations.

---

## 11. How AWS Global Infrastructure Works in a Real Application

Imagine you are building an e-learning platform using:

- Next.js frontend
- Node.js backend
- MySQL database
- Images and other uploaded files
- Students from different countries

A simplified architecture might look like this:

```text
                  GLOBAL USERS
                       |
                       v
                Amazon CloudFront
                 (Edge Locations)
                       |
                       v
             Application Load Balancer
                       |
              +--------+--------+
              |                 |
              v                 v
         EC2 Instance       EC2 Instance
              |                 |
             AZ-A              AZ-B
              |                 |
              +--------+--------+
                       |
                       v
                 Amazon RDS
                  (MySQL)
                       |
                       v
                  Amazon S3
               (Images and Files)
```

This is a conceptual architecture. In a real deployment, the database, networking and other dependencies must also be designed for security, availability and recovery.

### Request Flow

1. A student opens your website.
2. CloudFront may serve cached static files from a nearby Edge Location.
3. Requests that reach the application are distributed by the load balancer.
4. The Node.js backend processes the requests on EC2 instances.
5. The backend retrieves or updates data in MySQL.
6. Uploaded images and files are stored in Amazon S3.
7. CloudFront may deliver eligible files from its cache.

### Benefits of This Architecture

- Better content delivery performance.
- Distribution of application workloads.
- Improved resilience through multiple AZs.
- Scalable application infrastructure.
- Centralised object storage.

---

## 12. How to Choose an AWS Region

Consider these five factors when selecting a Region.

| Factor | Explanation |
|---|---|
| Latency | Consider the location of your users. |
| Cost | Service prices can vary across Regions. |
| Service Availability | Some services and features may not be available everywhere. |
| Compliance | Consider applicable data residency and regulatory requirements. |
| Disaster Recovery | Consider another Region if your recovery objectives require it. |

### Example

If most of your customers are in Germany, Frankfurt (`eu-central-1`) may be a reasonable starting point.

If your users are primarily in Bangladesh, compare suitable nearby Regions based on latency, cost, available services and compliance requirements.

**Important:** The geographically closest Region is not necessarily the best choice for every application.

---

## 13. How to Explore AWS Global Infrastructure

### Step 1: Open the AWS Management Console

Visit:

https://console.aws.amazon.com/

### Step 2: Find the Region Selector

Explore the Region selector near the top of the console.

For example, select:

- US East (N. Virginia)
- Europe (Frankfurt)
- Asia Pacific (Mumbai)

Notice how the selected Region affects the context in which you create and view many AWS resources.

Changing the selected Region does not move existing resources to another Region.

### Step 3: Explore EC2

Open the EC2 service and examine the available Region and Availability Zone information.

You can explore the infrastructure documentation without launching any resources.

### Official Documentation

- AWS Global Infrastructure: https://aws.amazon.com/about-aws/global-infrastructure/
- AWS Regions: https://docs.aws.amazon.com/global-infrastructure/latest/regions/aws-regions.html
- AWS Regions and Availability Zones: https://docs.aws.amazon.com/global-infrastructure/latest/regions/aws-regions-availability-zones.html

---

## 14. Interview Questions and Answers

### Q1. What is AWS Global Infrastructure?

AWS Global Infrastructure is the worldwide network of Regions, Availability Zones, data centres and edge infrastructure used to deliver AWS cloud services.

### Q2. What is an AWS Region?

An AWS Region is a separate geographical area where AWS operates its cloud infrastructure. It contains multiple Availability Zones.

### Q3. What is an Availability Zone?

An Availability Zone is an isolated location within an AWS Region. It consists of one or more data centres.

### Q4. What is the difference between a Region and an Availability Zone?

A Region is a geographical area, whereas an Availability Zone is an isolated location within that Region. Multiple AZs can improve application availability and resilience.

### Q5. Why should an application run across multiple Availability Zones?

Deploying an application across multiple AZs can reduce dependence on a single location and improve availability when one AZ experiences a failure.

### Q6. What is an Edge Location?

An Edge Location is a site within AWS's edge network that helps deliver content closer to users. Amazon CloudFront uses edge locations to cache and distribute content.

### Q7. What is the difference between a Local Zone and an Availability Zone?

An Availability Zone is an isolated location within a Region, while a Local Zone extends selected AWS infrastructure closer to a metropolitan area.

### Q8. What is AWS Wavelength?

AWS Wavelength brings selected AWS services into telecommunications providers' 5G networks to support low-latency applications.

### Q9. Does AWS automatically replicate data between Regions?

No. Cross-Region replication depends on the service and its configuration. Developers must configure replication or recovery mechanisms when required.

### Q10. What happens if one Availability Zone fails?

Resources in that AZ may become unavailable. An application designed for multi-AZ operation may continue serving users through the remaining AZs if its dependencies, capacity and failover mechanisms are configured correctly.

### Q11. What factors influence Region selection?

The main factors are latency, cost, service availability, compliance requirements and disaster recovery needs.

### Q12. What is the difference between a Data Centre and an Availability Zone?

A data centre is a physical facility containing computing equipment. An Availability Zone is an isolated infrastructure location that may consist of multiple data centres.

---

## 15. Quick Revision Notes

### Six Key Concepts

1. **AWS Global Infrastructure:** AWS's worldwide cloud infrastructure.
2. **Region:** A separate geographical area.
3. **Availability Zone:** An isolated location within a Region.
4. **Data Centre:** A physical facility containing computing equipment.
5. **Edge Location:** Helps deliver content closer to users.
6. **Local Zone and Wavelength Zone:** Bring selected AWS services closer to specific users, metropolitan areas or 5G networks.

### Conceptual Structure

```text
AWS GLOBAL INFRASTRUCTURE
|
|--- Regions
|     |
|     |--- Availability Zones
|             |
|             |--- One or more Data Centres
|
|--- Edge Locations
|
|--- Local Zones
|
|--- Wavelength Zones
```

**Note:** This is a conceptual overview. Edge Locations, Local Zones and Wavelength Zones are not simply lower levels in the Region hierarchy.

### Remember These Differences

- **Region:** Where you deploy your infrastructure geographically.
- **Availability Zone:** Where you distribute workloads for resilience within a Region.
- **Data Centre:** Where physical computing equipment is housed.
- **Edge Location:** Where eligible content can be cached closer to users.
- **Local Zone:** Where selected infrastructure can run near a metropolitan area.
- **Wavelength Zone:** Where selected AWS services can run within a 5G telecommunications network.

---

## 16. What to Learn Next

After understanding AWS Global Infrastructure, follow this learning sequence:

1. AWS Fundamentals
2. AWS Global Infrastructure
3. Amazon EC2 — Virtual Servers
4. Amazon S3 — Object Storage
5. AWS IAM — Identity and Access Management
6. Amazon VPC — Virtual Networking
7. Load Balancing and Auto Scaling
8. Amazon RDS — Managed Databases
9. Docker and Containerisation
10. Kubernetes and Container Orchestration
11. CI/CD and Cloud Deployment
12. Cloud Security and Monitoring

**Recommended next topic: Amazon EC2 (Elastic Compute Cloud).**

Learn how to launch virtual servers, choose instance types, configure security groups and deploy a Node.js backend.
