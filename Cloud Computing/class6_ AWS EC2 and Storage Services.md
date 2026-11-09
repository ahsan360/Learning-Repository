# AWS EC2 and Storage Services – Beginner to Production Guide

## 1. Introduction to AWS EC2

### What is EC2?

EC2 stands for **Elastic Compute Cloud**.

It is an AWS service that allows you to rent virtual computers (servers) from Amazon and run your applications on them.

For example, imagine you have developed a Next.js application with a Node.js backend.

Instead of purchasing a physical server, you can rent a virtual server from AWS. This virtual server is called an **EC2 instance**.

### What can you do with EC2?

- Host Next.js applications.
- Run Node.js and Python backends.
- Install MongoDB and MySQL.
- Run Docker containers.
- Configure Nginx.
- Deploy production applications.
- Run background jobs.
- Host APIs and microservices.

### EC2 Architecture

| Component | Purpose |
|---|---|
| VPC | Your private network in AWS |
| Subnet | A smaller network inside your VPC |
| EC2 | Your virtual server |
| Security Group | Controls incoming and outgoing traffic |
| Public IP | Allows internet communication |
| SSH | Allows remote access to your Linux server |
| EBS | Provides persistent disk storage for EC2 |

---

## 2. How to Access an EC2 Instance

There are several ways to access an EC2 instance.

The most important methods are:

1. SSH (Secure Shell)
2. EC2 Instance Connect
3. AWS Systems Manager Session Manager

### Method 1: SSH

SSH stands for **Secure Shell**.

It is a secure protocol that allows you to connect to and control a remote Linux server through your terminal.

For example:
- Your laptop is in Bangladesh.
- Your EC2 server is running in an AWS data centre in Europe.
- You want to install Node.js on that server.

You can use SSH to control that server remotely.

### Step 1: Create an EC2 Instance

Open the AWS EC2 Console:

https://console.aws.amazon.com/ec2/

Follow these steps:

1. Click Launch Instance.
2. Give your instance a name, such as `my-first-server`.
3. Select Ubuntu Server.
4. Choose an instance type, such as `t2.micro`, if available.
5. Create or select a key pair.
6. Select your VPC and subnet.
7. Enable a public IP address if you need direct internet access.
8. Configure the security group.
9. Launch the instance.

### Step 2: Understand the Key Pair

An EC2 key pair consists of two keys:

| Key | Purpose |
|---|---|
| Public Key | Stored on the EC2 server |
| Private Key | Downloaded and stored on your computer |

Example private key:

```text
my-server.pem
```

**Important:** Never share your `.pem` file or upload it to GitHub.

### Step 3: Configure the Security Group

Your EC2 instance needs permission to receive SSH connections.

Add this inbound rule:

| Type | Port | Source |
|---|---|---|
| SSH | 22 | My IP |

Port 22 is the default SSH port.

Avoid allowing SSH from `0.0.0.0/0` in production because it exposes your server to connection attempts from anywhere.

### Step 4: Connect from Windows

Open PowerShell.

Navigate to the directory containing your `.pem` file:

```powershell
cd Downloads
```

Connect using:

```bash
ssh -i "my-server.pem" ubuntu@YOUR_PUBLIC_IP
```

Replace `YOUR_PUBLIC_IP` with your EC2 public IPv4 address.

Default usernames:

| Operating System | Username |
|---|---|
| Ubuntu | ubuntu |
| Amazon Linux | ec2-user |

If the connection succeeds, you will see a terminal connected to your remote Linux machine.

### Step 5: Execute Linux Commands

Try these commands:

```bash
# Check current user
whoami

# Check operating system
cat /etc/os-release

# Check server IP
hostname -I

# Check available memory
free -h

# Check disk space
df -h

# Check CPU information
lscpu

# Update packages
sudo apt update
```

---

## 3. EC2 Instance Connect

EC2 Instance Connect allows you to connect to your EC2 instance directly from the AWS Management Console.

General process:

1. Open EC2.
2. Select your instance.
3. Click Connect.
4. Select EC2 Instance Connect.
5. Click Connect.

You can access your Linux terminal through your browser.

However, the network configuration, security group, operating system and EC2 Instance Connect prerequisites must be correct.

### Comparison of Access Methods

| Method | Best Use |
|---|---|
| SSH | Regular server administration |
| EC2 Instance Connect | Quick browser-based access |
| Systems Manager Session Manager | Managed access without requiring an inbound SSH port |

---

# 4. AWS Storage Services

Imagine you have deployed a Next.js application on EC2.

Your application needs to store:

- User profile pictures.
- PDF documents.
- Videos.
- Database files.
- Application logs.
- Backups.
- Uploaded files.

AWS provides different storage services for different purposes.

The three important services are:

1. Amazon S3
2. Amazon EBS
3. Amazon EFS

---

## 4.1 Amazon S3 (Simple Storage Service)

S3 is an object storage service.

You can store almost any type of file in S3.

### Real-world Example

Imagine you are developing an educational SaaS platform.

Your users upload:

- Profile pictures.
- Course thumbnails.
- Video files.
- PDF documents.
- Assignment files.

Instead of storing all these files on your EC2 server, you can store them in S3.

### Important S3 Terminology

#### 1. Bucket

A bucket is a container where you store objects.

Example:

```text
my-production-storage
```

#### 2. Object

An object is an individual file stored inside an S3 bucket.

Examples:

```text
profile.png
course-thumbnail.jpg
document.pdf
```

#### 3. Object Key

An object key is the unique identifier of an object within a bucket.

Example:

```text
users/101/profile.png
courses/500/thumbnail.jpg
documents/assignment.pdf
```

### Example S3 Structure

```text
my-production-storage/
│
├── users/
│   ├── 101/
│   │   └── profile.png
│   └── 102/
│       └── profile.png
│
├── courses/
│   ├── 500/
│   │   └── thumbnail.jpg
│   └── 501/
│       └── thumbnail.jpg
│
└── documents/
    └── assignment.pdf
```

**Important:** S3 does not use traditional directories like your computer. These folder-like structures are generally created using object key prefixes.

### When Should You Use S3?

| Use Case | Example |
|---|---|
| Images | User profile pictures |
| Videos | Course videos |
| Documents | PDF files |
| Backups | Database backups |
| Static files | CSS, JavaScript and assets |
| Logs | Application log archives |

---

## 4.2 Amazon EBS (Elastic Block Store)

EBS provides block storage for EC2 instances.

Think of EBS as an external hard drive attached to your virtual server.

For example:

Your EC2 instance has an operating system, application code and other files.

These files need disk storage.

EBS provides that storage.

### Example

```text
EC2 Instance
    |
    |
    +---- EBS Volume
              |
              +---- Ubuntu OS
              +---- Application Code
              +---- Installed Packages
              +---- Application Data
```

### Important EBS Concepts

| Concept | Explanation |
|---|---|
| Volume | A virtual block storage device |
| Snapshot | A point-in-time backup of an EBS volume |
| Volume Type | Determines performance characteristics |
| IOPS | Input/output operations per second |
| Throughput | Amount of data transferred per second |

### Common EBS Volume Types

| Type | Purpose |
|---|---|
| gp3 | General-purpose SSD |
| gp2 | Previous-generation general-purpose SSD |
| io1 | Provisioned IOPS SSD |
| io2 | High-performance Provisioned IOPS SSD |
| st1 | Throughput-optimised HDD |
| sc1 | Cold HDD |

For most beginner production applications, gp3 is a sensible starting point.

### When Should You Use EBS?

- EC2 operating system storage.
- Application files.
- Database storage.
- Persistent disk storage.
- Files requiring block-level access.

**Important:** EBS volumes are generally attached to EC2 instances in the same Availability Zone.

---

## 4.3 Amazon EFS (Elastic File System)

EFS is a managed network file system.

It allows multiple EC2 instances to access shared files.

Imagine you have three EC2 instances:

```text
EC2 Instance 1
       |
EC2 Instance 2 ---- EFS
       |
EC2 Instance 3
```

All three instances can access the same shared file system.

### When Should You Use EFS?

- Multiple EC2 instances need shared files.
- Shared application directories.
- Content management systems.
- Shared processing environments.
- Applications requiring a common file system.

---

# 5. S3 vs EBS vs EFS

This is an important comparison for AWS certification exams and production engineering.

| Feature | S3 | EBS | EFS |
|---|---|---|---|
| Storage Type | Object | Block | File |
| Main Purpose | Store files | EC2 disk storage | Shared file storage |
| Access | API/HTTP | Attached to EC2 | Network file system |
| Multiple EC2 Access | Yes, through APIs | Normally one EC2 at a time, with specific multi-attach exceptions | Yes |
| Example | Images and videos | OS and database disk | Shared application files |

### Simple Way to Remember

- **S3:** Store files.
- **EBS:** Attach a disk to EC2.
- **EFS:** Share files across multiple servers.

---

# 6. Practical Learning Roadmap

Follow these exercises in order.

| Exercise | Task |
|---|---|
| 1 | Launch an Ubuntu EC2 instance |
| 2 | Connect using SSH |
| 3 | Execute basic Linux commands |
| 4 | Install Node.js and Nginx |
| 5 | Deploy a simple Node.js application |
| 6 | Create an S3 bucket |
| 7 | Upload files to S3 |
| 8 | Connect EC2 to S3 using an IAM Role |
| 9 | Create an EBS volume |
| 10 | Attach and mount the EBS volume |
| 11 | Create an EBS snapshot |
| 12 | Explore EFS and mount it on EC2 |

## 7. Important Security Practices

1. Never expose your private SSH key.
2. Avoid public SSH access from `0.0.0.0/0`.
3. Never make an S3 bucket public without a clear requirement.
4. Use IAM Roles instead of hardcoding AWS access keys on EC2.
5. Take regular database and storage backups.
6. Monitor AWS costs.
7. Use HTTPS for production applications.
8. Apply the principle of least privilege.

## 8. What You Should Learn Next

After understanding EC2 and storage, learn:

1. IAM Roles and EC2 instance profiles.
2. AWS S3 bucket policies.
3. S3 versioning and lifecycle policies.
4. EBS snapshots and volume resizing.
5. Load Balancers.
6. Auto Scaling Groups.
7. Route 53.
8. CloudWatch monitoring.
9. Systems Manager.
10. AWS Backup.

**Your first practical goal:** Launch an Ubuntu EC2 instance, connect to it through SSH, create an S3 bucket, and upload a file from your EC2 server to S3.

Official documentation:

- EC2: https://docs.aws.amazon.com/ec2/
- S3: https://docs.aws.amazon.com/s3/
- EBS: https://docs.aws.amazon.com/ebs/
- EFS: https://docs.aws.amazon.com/efs/
