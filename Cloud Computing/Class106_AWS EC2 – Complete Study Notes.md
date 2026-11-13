# AWS EC2 – Complete Study Notes

**Topics:** EC2 Fundamentals, AMI, Instance Types, Instance Lifecycle and EC2 Pricing

---

# 1. What is Amazon EC2?

**EC2 stands for Elastic Compute Cloud.**

Amazon EC2 is an AWS service that provides resizable computing capacity through virtual servers in the cloud.

Instead of purchasing and maintaining physical servers, you can rent virtual machines from AWS.

### Real-world example

Suppose you want to deploy a Next.js application with a Node.js backend.

You need:
- CPU
- RAM
- Storage
- Operating system
- Networking

You can launch an EC2 instance, install Ubuntu, configure Node.js and deploy your application.

### Important concepts

| Term | Meaning |
|---|---|
| EC2 | Virtual server service |
| Elastic | Ability to adjust computing capacity |
| Instance | A virtual machine |
| vCPU | Virtual processing unit |
| RAM | Temporary memory |
| EBS | Persistent block storage |

**Exam tip:** EC2 provides scalable computing capacity in the AWS cloud.

---

# 2. What is an AMI?

**AMI stands for Amazon Machine Image.**

An AMI is a template used to launch EC2 instances.

Think of it as a reusable server blueprint.

### Example

You create an EC2 instance and install:

1. Ubuntu
2. Node.js
3. Nginx
4. Docker
5. Required dependencies

Now you want to launch another server with exactly the same configuration.

Instead of installing everything again, you can create an AMI from your configured instance and use it to launch additional instances.

### What does an AMI contain?

An AMI provides three important components:

| Component | Explanation |
|---|---|
| Root volume template | Operating system and root disk contents |
| Launch permissions | Who can use the AMI |
| Block device mapping | Storage volumes attached when launching the instance |

### Types of AMIs

- **AWS-provided AMIs:** Images provided by AWS.
- **Marketplace AMIs:** Images provided by third-party vendors.
- **Community AMIs:** Images shared publicly by other users.
- **Custom AMIs:** Images created by users.

### Important exam facts

- AMIs are Region-specific.
- You can create your own custom AMIs.
- You can share AMIs with other AWS accounts.
- You can copy AMIs between Regions.
- An AMI is not a running server.

**Remember:** AMI = Blueprint; EC2 instance = Actual virtual server.

---

# 3. EC2 Instance Types

An EC2 instance type determines the hardware resources available to your virtual server.

These resources include:

- CPU
- RAM
- Storage
- Network performance

Different applications require different hardware configurations.

## Five major instance categories

### 3.1 General Purpose

Provides a balanced combination of CPU, memory and networking.

**Use cases:**
- Web servers
- Development environments
- Small databases
- General applications

**Examples:** T3, T4g, M7i

### 3.2 Compute Optimized

Designed for applications requiring high CPU performance.

**Use cases:**
- Batch processing
- Gaming servers
- Scientific modelling
- High-performance web servers

**Examples:** C7i, C8g

### 3.3 Memory Optimized

Designed for applications requiring large amounts of RAM.

**Use cases:**
- In-memory databases
- Real-time analytics
- Caching
- Large database workloads

**Examples:** R7i, X2idn

### 3.4 Accelerated Computing

Uses hardware accelerators such as GPUs.

**Use cases:**
- Artificial intelligence
- Machine learning
- Graphics processing
- Deep learning

**Examples:** P5, G6, Inf2

### 3.5 Storage Optimized

Designed for workloads requiring high-speed local storage and high disk throughput.

**Use cases:**
- Data warehousing
- Distributed file systems
- High-performance databases
- Large-scale data processing

**Examples:** I4i, Im4gn, D3

## Instance family cheat sheet

| Family | Category |
|---|---|
| T, M | General Purpose |
| C | Compute Optimized |
| R, X | Memory Optimized |
| P, G, Inf | Accelerated Computing |
| I, D | Storage Optimized |

## Understanding instance naming

Example: `m7i.large`

| Part | Meaning |
|---|---|
| m | Instance family |
| 7 | Generation |
| i | Instance variant |
| large | Instance size |

Common instance sizes:

- nano
- micro
- small
- medium
- large
- xlarge
- 2xlarge
- 4xlarge

Generally, larger sizes provide more resources, although specifications depend on the instance family.

---

# 4. EC2 Instance Lifecycle

An EC2 instance passes through several lifecycle states.

## Six important states

| State | Meaning |
|---|---|
| Pending | AWS is preparing the instance |
| Running | Instance is operational |
| Stopping | AWS is stopping the instance |
| Stopped | Instance is powered off |
| Shutting-down | Instance is being terminated |
| Terminated | Instance has been permanently removed |

## Understanding each state

### 4.1 Pending

You request a new EC2 instance.

AWS prepares the virtual machine before making it available.

### 4.2 Running

Your virtual machine is operational.

You can connect using:
- SSH for Linux
- RDP for Windows

### 4.3 Stopping

You request AWS to stop a running instance.

### 4.4 Stopped

The instance is powered off.

You can start it again later.

### 4.5 Shutting-down

You request permanent termination of the instance.

### 4.6 Terminated

The instance has been permanently removed and cannot be restarted.

## Stop vs Terminate

| Feature | Stop | Terminate |
|---|---|---|
| Can restart? | Yes | No |
| Instance preserved? | Yes | No |
| Compute charges | Stop | Stop |
| EBS storage charges | Continue | Depend on deletion settings |
| Instance ID | Preserved | Permanently retired |

### What happens when you stop and restart an instance?

For an EBS-backed instance:

- Instance ID remains unchanged.
- Private IPv4 address is generally retained.
- Automatically assigned public IPv4 address is released.
- A new public IPv4 address is generally assigned when restarted.
- EBS volumes remain available.
- Instance-store data is lost.

**Important:** Use an Elastic IP address when you need a consistent public IPv4 address.

---

# 5. EC2 Pricing Models

This is one of the most important topics for AWS certification examinations.

AWS offers several purchasing options depending on your workload, budget and usage requirements.

There are five major pricing concepts you should understand.

## 5.1 On-Demand Instances

You pay for computing capacity according to your usage without making a long-term commitment.

**Characteristics:**
- No long-term commitment.
- No upfront payment required.
- Pay for the capacity you use.
- Flexible and easy to start or stop.

**Best for:**
- Short-term projects
- Unpredictable workloads
- Development and testing
- Applications with changing usage

**Example:**

You launch an EC2 instance for a temporary project and use it for 10 hours.

You pay for the applicable usage period.

**Exam keyword:** No long-term commitment.

## 5.2 Reserved Instances

You commit to a one-year or three-year term in exchange for discounted pricing compared with On-Demand rates.

**Characteristics:**
- One-year or three-year commitment.
- Significant potential savings.
- Suitable for predictable workloads.
- Payment options include No Upfront, Partial Upfront and All Upfront.

**Best for:**
- Production databases
- Consistent web servers
- Applications running continuously
- Predictable workloads

**Example:**

Your company runs the same application throughout the year.

Instead of paying On-Demand rates, you purchase a Reserved Instance to reduce costs.

**Exam keyword:** Long-term commitment and predictable workloads.

Note: Standard Reserved Instances have limited modification flexibility, while Convertible Reserved Instances offer greater flexibility.

## 5.3 Spot Instances

Spot Instances allow you to use unused AWS EC2 capacity at potentially substantial discounts compared with On-Demand prices.

However, AWS can interrupt your Spot Instance when it needs the capacity back.

AWS generally provides a two-minute interruption notice.

**Characteristics:**
- Potentially very low cost.
- Uses spare AWS capacity.
- Can be interrupted by AWS.
- Not suitable for workloads requiring uninterrupted availability.

**Best for:**
- Batch processing
- Data analysis
- Background jobs
- Fault-tolerant applications
- Large-scale testing

**Example:**

You have 1,000 independent background jobs.

If one server is interrupted, another server can continue the remaining work.

Spot Instances can significantly reduce costs.

**Exam keyword:** Cheapest potential option, but interruptible.

## 5.4 Savings Plans

Savings Plans provide lower prices in exchange for committing to a consistent amount of eligible compute usage, measured in dollars per hour, over a one-year or three-year term.

There are two important types:

### Compute Savings Plans

- Flexible across EC2 instance families.
- Flexible across instance sizes.
- Flexible across AWS Regions.
- Can also apply to eligible AWS Fargate and Lambda usage.

### EC2 Instance Savings Plans

- Apply to a specific EC2 instance family in a specific Region.
- Offer greater potential discounts.
- Less flexible than Compute Savings Plans.

**Best for:** Organizations with consistent long-term compute usage that want pricing flexibility.

**Exam keyword:** Commitment to a consistent hourly spend.

## 5.5 Dedicated Hosts and Dedicated Instances

These options are important when an organization requires dedicated physical infrastructure.

### Dedicated Hosts

A physical EC2 server dedicated to a single customer.

Useful for:
- Software licensing requirements.
- Regulatory compliance.
- Host-level visibility.
- Specific enterprise licensing arrangements.

### Dedicated Instances

EC2 instances running on hardware dedicated to a single customer.

However, they do not provide the same level of host-level visibility and control as Dedicated Hosts.

**Remember:** Dedicated Host = Dedicated physical server with host-level control and visibility.

---

# 6. EC2 Pricing Comparison

| Pricing model | Commitment | Cost advantage | Main limitation |
|---|---|---|---|
| On-Demand | None | Flexible | Higher standard rates |
| Reserved Instances | 1 or 3 years | Discounts | Less flexibility |
| Spot Instances | No fixed term | Potentially highest savings | Can be interrupted |
| Savings Plans | 1 or 3 years | Discounts | Hourly usage commitment |
| Dedicated Hosts | Varies | Licensing benefits | Dedicated hardware costs |

## Which pricing model should you choose?

| Scenario | Best option |
|---|---|
| Temporary testing environment | On-Demand |
| Application running 24/7 | Reserved Instances or Savings Plans |
| Interruptible background jobs | Spot Instances |
| Flexible long-term compute usage | Compute Savings Plans |
| Specific physical server licensing requirements | Dedicated Hosts |

---

# 7. Additional EC2 Pricing Considerations

The cost of an EC2 instance is not limited to CPU and RAM.

You should understand these additional charges.

### 7.1 EBS Storage

Amazon EBS provides persistent block storage for EC2 instances.

You generally pay for allocated storage, and additional charges may apply for provisioned performance and other features.

Important distinction:

Stopping an EBS-backed EC2 instance does not automatically stop EBS storage charges.

### 7.2 Data Transfer

AWS can charge for certain data transfers, depending on the source, destination and service.

For example:
- Data transferred out to the internet can incur charges.
- Data transferred into AWS is generally free.
- Data transfer between services and Regions has specific pricing rules.

### 7.3 Elastic IP Address

AWS charges for public IPv4 addresses, including Elastic IP addresses, under its public IPv4 pricing policy.

Do not assume that an Elastic IP is always free.

### 7.4 Instance Store

Instance Store provides temporary storage physically attached to the host.

Important:
- Data is temporary.
- Data is lost when the instance is stopped or terminated.
- It is not a replacement for persistent EBS storage.

---

# 8. AWS Exam Preparation – Important Facts

Memorise these concepts:

| Question | Answer |
|---|---|
| What is EC2? | Virtual computing service |
| What is an AMI? | Template for launching EC2 instances |
| Which family is CPU-intensive? | C |
| Which family is memory-intensive? | R |
| Which family is GPU-oriented? | P and G |
| Which family is storage optimized? | I and D |
| Cheapest potential EC2 purchasing option? | Spot |
| Best for unpredictable workloads? | On-Demand |
| Best for predictable long-term usage? | Reserved Instances or Savings Plans |
| Can a stopped instance restart? | Yes |
| Can a terminated instance restart? | No |
| What is an Elastic IP? | Static public IPv4 address |
| Does EBS storage incur charges when EC2 is stopped? | Yes |
| What happens to instance-store data after stopping? | It is lost |

---

# 9. Practice Questions

Test your knowledge with these AWS certification-style questions.

### Question 1

A company needs to run a web application with unpredictable traffic. It does not want to make a long-term financial commitment.

Which purchasing option should it choose?

A. Reserved Instances  
B. Spot Instances  
C. On-Demand Instances  
D. Dedicated Hosts

**Correct answer: C. On-Demand Instances**

Explanation: On-Demand is suitable for unpredictable workloads without long-term commitments.

### Question 2

A company needs EC2 instances for batch processing. The workload can tolerate interruptions.

Which pricing model is the most appropriate?

A. On-Demand  
B. Reserved Instances  
C. Spot Instances  
D. Dedicated Hosts

**Correct answer: C. Spot Instances**

Explanation: Spot Instances use unused AWS capacity and can offer substantial cost savings. They can be interrupted.

### Question 3

A company operates a large in-memory database.

Which EC2 instance family should it choose?

A. C  
B. R  
C. T  
D. G

**Correct answer: B. R**

Explanation: Memory-optimized instances are suitable for applications requiring substantial RAM.

### Question 4

A developer wants to temporarily shut down an EC2 instance without losing its EBS data.

What should the developer do?

A. Terminate the instance  
B. Delete the AMI  
C. Stop the instance  
D. Delete the EBS volume

**Correct answer: C. Stop the instance**

Explanation: Stopping an EBS-backed instance preserves its EBS volumes.

### Question 5

A company needs a physical server dedicated to its AWS account because of software licensing requirements.

Which option should it choose?

A. Spot Instances  
B. Dedicated Hosts  
C. On-Demand Instances  
D. General Purpose Instances

**Correct answer: B. Dedicated Hosts**

Explanation: Dedicated Hosts provide dedicated physical servers and host-level visibility.

### Question 6

A company has a stable workload and wants to reduce EC2 costs through a one-year commitment while retaining flexibility across instance families and Regions.

Which option is most appropriate?

A. Standard Reserved Instances  
B. Spot Instances  
C. Compute Savings Plans  
D. Dedicated Instances

**Correct answer: C. Compute Savings Plans**

Explanation: Compute Savings Plans offer flexibility across EC2 families, sizes and Regions, as well as eligible Fargate and Lambda usage.

### Question 7

What happens to an automatically assigned public IPv4 address when an EBS-backed EC2 instance is stopped?

A. It remains permanently assigned  
B. It is released  
C. The instance is terminated  
D. The EBS volume is deleted

**Correct answer: B. It is released**

Explanation: A new public IPv4 address is generally assigned when the instance restarts.

### Question 8

A developer stops an EC2 instance. Which charge may continue?

A. EC2 compute charges  
B. EBS storage charges  
C. Both must stop  
D. Neither can continue

**Correct answer: B. EBS storage charges**

Explanation: Stopping an EC2 instance stops its compute charges, but persistent EBS volumes can continue to incur storage charges.

---

# 10. Final Revision Cheat Sheet

Remember these five fundamental concepts:

1. **EC2:** A virtual server in AWS.
2. **AMI:** A reusable template for launching EC2 instances.
3. **Instance Types:** Determine CPU, memory, storage and networking resources.
4. **Lifecycle:** Pending → Running → Stopping → Stopped; termination is a separate permanent shutdown process.
5. **Pricing:** On-Demand, Reserved Instances, Spot Instances, Savings Plans and Dedicated Hosts.

## My recommendation

Do not memorise everything without understanding it.

For each AWS service:
1. Understand what problem it solves.
2. Understand how it works.
3. Learn its real-world use cases.
4. Understand the differences between similar services.
5. Practise scenario-based examination questions.

**Your objective is to understand AWS well enough to select the correct service or configuration when presented with a real-world business scenario.**
