# AWS Shared Responsibility Model

## 1. What is the Shared Responsibility Model?

The AWS Shared Responsibility Model explains how security responsibilities are divided between AWS and its customers.

- AWS is responsible for **Security of the Cloud**.
- Customers are responsible for **Security in the Cloud**.

## 2. AWS Responsibilities (Security of the Cloud)

AWS protects the underlying cloud infrastructure.

Examples:
- Physical data centres
- Physical servers and hardware
- Networking infrastructure
- Infrastructure supporting AWS services

## 3. Customer Responsibilities (Security in the Cloud)

Customers protect their data, applications, and configurations.

Examples:
- Managing user permissions
- Protecting passwords and credentials
- Configuring firewalls and security groups
- Updating operating systems
- Securing applications
- Protecting customer data

## 4. Practical Example: Amazon EC2

Suppose you deploy a website on an Amazon EC2 virtual server.

| Responsibility | Responsible Party |
|---|---|
| Physical server security | AWS |
| Data centre security | AWS |
| Operating system updates | Customer |
| Application security | Customer |
| User access permissions | Customer |
| Customer data protection | Customer |

**Note:** Responsibilities may vary depending on the AWS service being used.

## 5. Important Concept to Remember

- AWS = Security OF the Cloud.
- Customer = Security IN the Cloud.

**Remember:** AWS secures the cloud infrastructure, while customers secure what they deploy and configure in the cloud.
