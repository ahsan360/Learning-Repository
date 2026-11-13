# AWS EC2 Auto Scaling

## 1. What is EC2 Auto Scaling?

Amazon EC2 Auto Scaling is an AWS service that automatically increases or decreases the number of EC2 instances according to application demand.

In simple words:

- When traffic increases, AWS launches additional EC2 instances.
- When traffic decreases, AWS terminates unnecessary EC2 instances.
- When an instance becomes unhealthy, AWS can replace it automatically.

### Why do we use EC2 Auto Scaling?

1. **High Availability:** Maintains application availability.
2. **Scalability:** Automatically adjusts computing capacity.
3. **Cost Optimisation:** Avoids paying for unnecessary instances.
4. **Fault Tolerance:** Replaces unhealthy EC2 instances.
5. **Performance:** Handles changing workloads efficiently.

### Example

Suppose you have an e-commerce application running on EC2.

- Normal traffic: 100 users → 1 EC2 instance.
- High traffic: 10,000 users → 5 EC2 instances.
- Low traffic: 50 users → 1 EC2 instance.

Auto Scaling automatically adjusts the number of EC2 instances according to demand.

---

## 2. Components of EC2 Auto Scaling

### 2.1 Launch Template

**What is it?**

A Launch Template is a blueprint that defines how AWS should create an EC2 instance.

It contains the configuration required to launch new EC2 instances.

**What does it contain?**

| Configuration | Description |
|---|---|
| AMI | Operating system image |
| Instance Type | Computing capacity, such as t3.micro |
| Key Pair | SSH access configuration |
| Security Group | Firewall rules |
| Storage | EBS volume configuration |
| User Data | Startup scripts |
| IAM Instance Profile | Permissions assigned to the instance |

**When do we use it?**

Whenever Auto Scaling needs to launch a new EC2 instance, it uses the Launch Template to determine the instance configuration.

**Example:**

- AMI: Amazon Linux
- Instance Type: t3.micro
- Storage: 8 GB
- Security Group: Web-server security group
- User Data: Install Nginx

Every instance launched using this template receives the specified configuration.

**Important:** Launch Templates are recommended over the older Launch Configurations.

### 2.2 Auto Scaling Group (ASG)

**What is it?**

An Auto Scaling Group is a logical group of EC2 instances managed together by AWS.

It controls how many EC2 instances should run in your application.

**Three important settings:**

| Setting | Meaning |
|---|---|
| Minimum Capacity | Minimum number of instances |
| Desired Capacity | Target number of instances |
| Maximum Capacity | Maximum number of instances |

**Example:**

Suppose you configure:

- Minimum: 2
- Desired: 3
- Maximum: 5

This means:

- AWS should maintain at least 2 instances.
- The initial target is 3 instances.
- AWS cannot scale beyond 5 instances.

When traffic increases, the number of instances can increase from 3 to 5.

When traffic decreases, the number can decrease from 5 to 3 or 2.

**When do we use it?**

When we want AWS to manage multiple EC2 instances automatically.

### 2.3 Scaling Policies

**What is it?**

A Scaling Policy defines when and how Auto Scaling should increase or decrease the number of EC2 instances.

There are four important scaling approaches.

#### A. Target Tracking Scaling

**What is it?**

Target Tracking automatically adjusts the number of EC2 instances to maintain a specific metric value.

**Example:**

- Target CPU utilisation: 50%.
- Current CPU utilisation: 85%.
- AWS launches additional EC2 instances.
- CPU utilisation decreases as workloads are distributed.

**When to use it?**

When you want to maintain a specific average metric, such as CPU utilisation.

#### B. Step Scaling

**What is it?**

Step Scaling adjusts the number of instances according to the severity of a CloudWatch alarm.

**Example:**

| CPU Utilisation | Scaling Action |
|---|---|
| 60% | Add 1 instance |
| 75% | Add 2 instances |
| 90% | Add 3 instances |

**When to use it?**

When different workload levels require different scaling actions.

#### C. Simple Scaling

**What is it?**

Simple Scaling adds or removes instances based on a CloudWatch alarm and a specified scaling adjustment.

It generally uses a cooldown period before another scaling action.

**When to use it?**

For straightforward scaling requirements.

#### D. Scheduled Scaling

**What is it?**

Scheduled Scaling changes the number of EC2 instances according to a predefined schedule.

**Example:**

- 9 AM: Increase capacity to 5 instances.
- 6 PM: Reduce capacity to 2 instances.

**When to use it?**

When application traffic follows predictable patterns.

---

### 2.4 Health Checks

**What are they?**

Health checks determine whether an EC2 instance is healthy or unhealthy.

Auto Scaling supports:

1. EC2 health checks.
2. Elastic Load Balancing health checks.

**Example:**

Suppose you have three EC2 instances:

- Instance A: Healthy.
- Instance B: Healthy.
- Instance C: Unhealthy.

If Auto Scaling detects that Instance C is unhealthy, it can terminate and replace it.

**When do we use it?**

To maintain application availability and automatically replace unhealthy instances.

---

### 2.5 Amazon CloudWatch

**What is it?**

Amazon CloudWatch is an AWS monitoring service that collects metrics, logs and events from AWS resources.

Auto Scaling uses CloudWatch metrics and alarms to trigger scaling actions.

**Common monitoring metrics:**

- CPU Utilisation
- Network In
- Network Out
- Application-specific metrics
- Memory utilisation (when configured through an appropriate monitoring agent)

**Example:**

1. CloudWatch monitors EC2 CPU utilisation.
2. CPU utilisation reaches 80%.
3. CloudWatch triggers an alarm.
4. The alarm activates a scaling policy.
5. Auto Scaling launches additional EC2 instances.

**When do we use it?**

To monitor AWS resources and trigger scaling actions based on metrics.

---

## 3. Additional Components Used with Auto Scaling

### 3.1 Elastic Load Balancer (ELB)

**What is it?**

A Load Balancer distributes incoming application traffic across multiple EC2 instances.

Instead of sending all requests to one EC2 instance, it distributes requests across available instances.

**How does it work with Auto Scaling?**

1. A user sends a request.
2. The Load Balancer receives the request.
3. It forwards the request to a healthy EC2 instance.
4. Auto Scaling launches additional instances when required.
5. Newly launched instances are registered with the target group and can receive traffic after passing health checks.

**When do we use it?**

When we want to distribute application traffic across multiple EC2 instances.

**Important:** Auto Scaling manages the number of EC2 instances. Load Balancing distributes traffic between them.

### 3.2 Availability Zones (AZs)

**What are they?**

Availability Zones are separate physical locations within an AWS Region.

An Auto Scaling Group can distribute EC2 instances across multiple Availability Zones.

**Example:**

- Region: ap-south-1 (Mumbai)
- Availability Zone: ap-south-1a
- Availability Zone: ap-south-1b

You can configure your Auto Scaling Group to launch instances in both Availability Zones.

**Why do we use them?**

- Improve application availability.
- Reduce the impact of an Availability Zone failure.
- Distribute application infrastructure across separate locations.

### 3.3 Cooldown Period

**What is it?**

A cooldown period is a waiting period after a scaling activity, primarily associated with Simple Scaling.

It prevents Auto Scaling from repeatedly performing scaling activities too quickly.

**Example:**

If the cooldown period is 300 seconds, Simple Scaling waits for that period before another scaling activity.

**When do we use it?**

When we want to prevent unnecessary repeated scaling actions.

### 3.4 Instance Warmup

**What is it?**

Instance warmup is the time required for a newly launched EC2 instance to initialise and become ready to handle workloads.

**Example:**

Your application takes 120 seconds to start.

You can configure an instance warmup period of 120 seconds.

**When do we use it?**

When newly launched instances need time to become operational before their metrics are used for certain scaling decisions.

---

## 4. Scale Out vs Scale In

### Scale Out

Scale Out means increasing the number of EC2 instances.

Example:

2 EC2 instances → 5 EC2 instances.

**When?** When application traffic or workload increases.

### Scale In

Scale In means decreasing the number of EC2 instances.

Example:

5 EC2 instances → 2 EC2 instances.

**When?** When application traffic or workload decreases.

### Horizontal Scaling vs Vertical Scaling

| Horizontal Scaling | Vertical Scaling |
|---|---|
| Adds or removes EC2 instances | Increases or decreases the capacity of an existing instance |
| Example: 2 → 5 instances | Example: t3.small → t3.large |
| Also called scaling out/in | Also called scaling up/down |

EC2 Auto Scaling primarily provides horizontal scaling.

---

## 5. How All Components Work Together

Consider a Node.js application hosted on AWS.

Initial configuration:

- Minimum instances: 2
- Desired instances: 2
- Maximum instances: 6
- Target CPU utilisation: 50%

### Workflow

1. Users start accessing the application.
2. CPU utilisation increases to 80%.
3. CloudWatch collects CPU metrics.
4. The scaling policy determines that additional capacity is required.
5. Auto Scaling launches additional EC2 instances using the Launch Template.
6. The Load Balancer distributes traffic across healthy instances.
7. Traffic eventually decreases.
8. Auto Scaling removes unnecessary instances.

This process is called Dynamic Scaling.

---

## 6. Types of EC2 Auto Scaling Policies

| Scaling Policy | Purpose | Example |
|---|---|---|
| Target Tracking | Maintain a target metric | Maintain 50% CPU utilisation |
| Step Scaling | Scale according to alarm severity | Add 1, 2 or 3 instances |
| Simple Scaling | Scale based on a single alarm and adjustment | Add 1 instance |
| Scheduled Scaling | Scale at predefined times | Increase capacity at 9 AM |

---

## 7. Important AWS Certification Exam Notes

| Question / Requirement | Correct Concept |
|---|---|
| Need to define EC2 instance configuration? | Launch Template |
| Need to manage multiple EC2 instances? | Auto Scaling Group |
| Need to maintain average CPU utilisation around 50%? | Target Tracking Scaling |
| Need different scaling adjustments based on alarm severity? | Step Scaling |
| Need to scale at a specific time? | Scheduled Scaling |
| Need to distribute traffic across EC2 instances? | Elastic Load Balancer |
| Need to monitor CPU utilisation? | CloudWatch |
| Need to replace unhealthy instances? | Auto Scaling Group Health Checks |
| Need instances across multiple locations? | Multiple Availability Zones |
| Need to increase the number of instances? | Scale Out |
| Need to decrease the number of instances? | Scale In |

### Important points to remember

1. Launch Template defines how EC2 instances are created.
2. Auto Scaling Group manages EC2 instances.
3. Scaling Policies determine when to scale.
4. CloudWatch monitors metrics and triggers alarms.
5. Load Balancer distributes incoming traffic.
6. Health Checks identify unhealthy instances.
7. Availability Zones improve availability.
8. Minimum, Desired and Maximum capacity control the number of instances.

---

## 8. Practical Hands-on Learning

Follow these steps to understand EC2 Auto Scaling practically.

- [ ] Create a Launch Template using an Amazon Linux AMI.
- [ ] Configure instance type, security group and user data.
- [ ] Create an Auto Scaling Group.
- [ ] Select two Availability Zones and subnets.
- [ ] Set minimum = 1, desired = 2, maximum = 3.
- [ ] Create an Application Load Balancer.
- [ ] Attach the Load Balancer target group to the Auto Scaling Group.
- [ ] Create a Target Tracking Scaling Policy.
- [ ] Generate test traffic and observe scaling.
- [ ] Terminate an EC2 instance and observe automatic replacement.
- [ ] Delete all resources after completing the exercise.

**Cost Warning:** EC2 instances, Application Load Balancers and related resources can incur charges. Monitor your AWS billing dashboard and delete resources after completing the exercise.

---

## 9. Quick Revision

| Component | One-line Definition |
|---|---|
| Launch Template | Blueprint for creating EC2 instances |
| Auto Scaling Group | Manages a group of EC2 instances |
| Scaling Policy | Defines when and how to scale |
| CloudWatch | Monitoring and alarm service |
| Load Balancer | Distributes incoming traffic |
| Health Checks | Identify unhealthy instances |
| Availability Zones | Separate physical locations in a Region |
| Cooldown | Waiting period associated with Simple Scaling |
| Instance Warmup | Time required for a new instance to initialise |
| Scale Out | Increase the number of instances |
| Scale In | Decrease the number of instances |

**Key takeaway:** EC2 Auto Scaling automatically adjusts the number of EC2 instances to meet application demand while improving availability, performance and cost efficiency.
