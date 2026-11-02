# AWS VPC and Subnets – Complete Beginner's Guide

# Part 1: Understanding Computer Networking

Before learning VPCs and subnets, you need to understand a few basic networking concepts.

## 1. What is a Network?

A network is a group of devices connected so that they can communicate and exchange information.

For example, imagine your home:

- Your laptop is connected to Wi-Fi.
- Your smartphone is connected to Wi-Fi.
- Your smart TV is connected to Wi-Fi.

All these devices are part of your home network.

They can communicate with each other and access the internet through your router.

AWS works similarly, but instead of connecting physical devices in your home, you create virtual networks for cloud resources.

## 2. What is an IP Address?

An IP address is a unique numerical address used to identify a device or network interface on a network.

Think of it as a home address.

Just as someone needs your home address to send you a parcel, computers use IP addresses to communicate with each other.

An example of an IPv4 address:

`192.168.1.10`

IPv4 addresses consist of four numbers separated by dots.

Each number ranges from 0 to 255.

Examples:

- 192.168.1.10
- 10.0.0.5
- 172.16.0.20

### Private and Public IP Addresses

There are two important categories of IPv4 addresses.

**Private IP address:**

Used for communication within private networks.

Examples of private IP ranges:

- 10.0.0.0 – 10.255.255.255
- 172.16.0.0 – 172.31.255.255
- 192.168.0.0 – 192.168.255.255

These addresses are not directly routable over the public internet.

**Public IP address:**

An address that can be reached over the public internet, subject to routing and security controls.

For example:

Your laptop might have a private IP address inside your home network, while your router uses a public IP address to communicate with the internet.

### Important Difference

| Private IP | Public IP |
|---|---|
| Used within private networks | Used for internet communication |
| Not directly routable over the public internet | Routable over the public internet |
| Commonly used for internal resources | Commonly used for publicly accessible resources |

## 3. What is a Network Range?

Imagine you have the following IP addresses:

- 10.0.0.1
- 10.0.0.2
- 10.0.0.3
- 10.0.0.4
- 10.0.0.5

Instead of configuring each address separately, you can define a network range that contains many IP addresses.

For example:

`10.0.0.0/24`

This represents a network containing 256 IPv4 addresses.

This brings us to an important networking concept called CIDR.

## 4. What is CIDR?

CIDR stands for **Classless Inter-Domain Routing**.

It is a method of representing IP address ranges.

Example:

`10.0.0.0/16`

Let's understand the notation.

- `10.0.0.0` is the network address.
- `/16` represents the number of bits reserved for the network portion.

An IPv4 address contains 32 bits.

Therefore:

- `/16` means 16 network bits and 16 host bits.
- `/24` means 24 network bits and 8 host bits.
- `/28` means 28 network bits and 4 host bits.

### Common CIDR Ranges

| CIDR | Total IPv4 Addresses |
|---|---:|
| /16 | 65,536 |
| /20 | 4,096 |
| /24 | 256 |
| /25 | 128 |
| /26 | 64 |
| /27 | 32 |
| /28 | 16 |

Formula:

`Total IPv4 addresses = 2^(32 - prefix length)`

For example:

`10.0.1.0/24`

Number of addresses:

`2^(32 - 24) = 2^8 = 256`

### What is the Difference Between /16 and /24?

A smaller prefix number means a larger network.

For example:

- /16 provides 65,536 addresses.
- /24 provides 256 addresses.

Therefore, a /16 network is much larger than a /24 network.

---

# Part 2: Understanding AWS VPC

## 5. What is AWS VPC?

VPC stands for **Virtual Private Cloud**.

Amazon VPC allows you to create a logically isolated virtual network inside AWS.

Inside this network, you can launch and manage resources such as:

- EC2 instances
- RDS databases
- Load balancers
- Other AWS networking resources

You control the network's IP address range, subnets, routing, and network security.

### Real-World Example

Imagine you are building an e-commerce application.

Your application requires:

1. A frontend that customers can access through the internet.
2. A backend server that processes orders.
3. A database that stores customer information.

You should not expose every component directly to the internet.

Instead, you can create an AWS VPC and divide it into different subnets.

For example:

- Public subnet: Internet-facing load balancer.
- Private subnet: Backend application servers.
- Private subnet: Database servers.

This creates a more secure and organised architecture.

## 6. Why Do We Need VPC?

Without proper network isolation and configuration, it becomes difficult to control how cloud resources communicate.

VPC provides several benefits.

### A. Network Isolation

You can create a logically isolated network for your application.

### B. IP Address Management

You can define your own private IP address range.

### C. Network Security

You can control network traffic using security groups and network ACLs.

### D. Internet Connectivity Control

You can decide which resources can communicate with the internet.

### E. Network Architecture

You can separate frontend, backend, and database resources into different subnets.

### F. Connectivity to Other Networks

You can connect your VPC to other networks using services such as:

- VPC Peering
- AWS Site-to-Site VPN
- AWS Direct Connect
- AWS Transit Gateway

## 7. Creating a VPC

Suppose you create a VPC with this CIDR block:

`10.0.0.0/16`

This means your VPC has 65,536 IPv4 addresses in its address range.

You can use these addresses to create smaller networks called subnets.

For example:

| Resource | CIDR |
|---|---|
| VPC | 10.0.0.0/16 |
| Public Subnet | 10.0.1.0/24 |
| Private Subnet | 10.0.2.0/24 |
| Database Subnet | 10.0.3.0/24 |

All three subnets belong to the same VPC.

Notice that their IP ranges do not overlap.

---

# Part 3: Understanding Subnets

## 8. What is a Subnet?

A subnet is a smaller IP network created inside a VPC.

Think of a VPC as a large office building.

Inside the building, you have different departments:

- Development department
- Testing department
- Finance department

Each department has its own responsibilities.

Similarly, a VPC can contain different subnets for different purposes.

For example:

- Public subnet for internet-facing resources.
- Private subnet for application servers.
- Private subnet for databases.

### Example

Suppose your VPC has this network:

`10.0.0.0/16`

You can divide it into smaller subnets:

| Subnet | CIDR | Purpose |
|---|---|---|
| Subnet A | 10.0.1.0/24 | Frontend |
| Subnet B | 10.0.2.0/24 | Backend |
| Subnet C | 10.0.3.0/24 | Database |

Each subnet has its own IP address range.

### Important Rules

1. Every subnet belongs to one VPC.
2. A subnet's CIDR must be within its VPC's IPv4 CIDR range.
3. Subnet CIDR ranges must not overlap within the same VPC.
4. Every subnet exists in exactly one Availability Zone.
5. A VPC can contain multiple subnets.

## 9. Public Subnet vs Private Subnet

This is one of the most important AWS networking concepts.

### A. Public Subnet

A public subnet is a subnet whose associated route table has a route to an Internet Gateway.

Example route:

| Destination | Target |
|---|---|
| 10.0.0.0/16 | local |
| 0.0.0.0/0 | Internet Gateway |

Here:

- `10.0.0.0/16` represents internal VPC communication.
- `0.0.0.0/0` represents all IPv4 destinations not covered by a more specific route.
- Internet Gateway provides the internet route.

For an EC2 instance to communicate directly with the public internet, it generally also needs a public IPv4 address or Elastic IP, along with appropriate security rules.

### B. Private Subnet

A private subnet does not have a direct route to an Internet Gateway.

Example:

| Destination | Target |
|---|---|
| 10.0.0.0/16 | local |
| 0.0.0.0/0 | NAT Gateway |

The NAT Gateway allows eligible resources in the private subnet to initiate outbound internet connections.

For example, a backend server can download software updates without being directly accessible through an inbound internet connection.

### Comparison

| Public Subnet | Private Subnet |
|---|---|
| Has a route to an Internet Gateway | Does not have a direct route to an Internet Gateway |
| Can host internet-facing resources | Commonly hosts backend servers and databases |
| Can support direct internet connectivity | Can use NAT Gateway for outbound internet access |
| Often contains load balancers | Often contains application servers |

**Important:** A subnet is not public simply because its IP range is public or private. Its routing configuration determines whether it is public or private.

---

# Part 4: Important VPC Components

## 10. Internet Gateway (IGW)

An Internet Gateway is a VPC component that enables communication between your VPC and the internet.

Imagine you have an EC2 instance in a public subnet.

For internet connectivity, you generally need:

1. An Internet Gateway attached to the VPC.
2. A route to the Internet Gateway.
3. A public IPv4 address or Elastic IP for direct IPv4 internet communication.
4. Appropriate security group and network ACL rules.

Example route table:

| Destination | Target |
|---|---|
| 10.0.0.0/16 | local |
| 0.0.0.0/0 | igw-123456 |

The second route sends internet-bound IPv4 traffic through the Internet Gateway.

**Remember:** An Internet Gateway provides the VPC's connection to the internet, but it does not automatically make every resource publicly accessible.

## 11. NAT Gateway

NAT stands for **Network Address Translation**.

A NAT Gateway allows resources in a private subnet to initiate connections to the internet without accepting unsolicited inbound internet connections.

### Real-World Example

Suppose your backend EC2 instance runs in a private subnet.

It needs to:

- Download software updates.
- Install application dependencies.
- Communicate with an external API.

However, you do not want the EC2 instance to be directly accessible from the internet.

You can use a NAT Gateway.

### How It Works

1. Your private EC2 instance sends a request to the internet.
2. The request goes through the NAT Gateway.
3. The NAT Gateway uses its public connectivity to communicate with the internet.
4. The response returns through the NAT Gateway.
5. The response reaches your EC2 instance.

### Important Points

- A public NAT Gateway is placed in a public subnet.
- It requires an Elastic IP address.
- The public subnet must have a route to an Internet Gateway.
- Private subnet route tables can direct internet-bound traffic to the NAT Gateway.
- A NAT Gateway does not allow unsolicited inbound internet connections to the private instance.

## 12. Route Table

A route table determines where network traffic should be directed.

Think of it as a navigation system.

When traffic needs to travel somewhere, the route table determines the appropriate destination.

### Example

| Destination | Target |
|---|---|
| 10.0.0.0/16 | local |
| 0.0.0.0/0 | igw-123456 |

Explanation:

**First route:**

`10.0.0.0/16 → local`

Allows communication within the VPC's IPv4 network.

**Second route:**

`0.0.0.0/0 → Internet Gateway`

Directs other IPv4 traffic towards the internet.

### Important Concepts

- Every subnet must be associated with a route table.
- A route table can be associated with multiple subnets.
- A subnet can be associated with only one route table at a time.
- Every VPC has a main route table.
- AWS uses the most specific matching route when choosing a route.

---

# Part 5: Availability Zones and Subnets

## 13. What is an Availability Zone?

An Availability Zone (AZ) is an isolated location within an AWS Region.

An AWS Region contains multiple Availability Zones.

For example, a Region may contain:

- Availability Zone A
- Availability Zone B
- Availability Zone C

Each subnet belongs to exactly one Availability Zone.

### Example

Suppose your VPC has two Availability Zones.

| Subnet | Availability Zone |
|---|---|
| Public Subnet A | AZ-1 |
| Private Subnet A | AZ-1 |
| Public Subnet B | AZ-2 |
| Private Subnet B | AZ-2 |

You can deploy resources across multiple AZs to improve availability.

If one Availability Zone experiences an outage, resources in another AZ may continue operating.

**Important:** A subnet cannot span multiple Availability Zones.

---

# Part 6: Security in VPC

## 14. Security Groups

A security group acts as a virtual firewall for an EC2 instance's network interface.

It controls inbound and outbound traffic.

### Example

Suppose your EC2 instance hosts a web application.

You might configure:

| Type | Port | Source |
|---|---:|---|
| HTTP | 80 | 0.0.0.0/0 |
| HTTPS | 443 | 0.0.0.0/0 |
| SSH | 22 | Your trusted IP address |

This allows public HTTP and HTTPS traffic but restricts SSH access to your trusted IP.

### Important Characteristics

- Security groups are stateful.
- They support allow rules, not explicit deny rules.
- They are associated with network interfaces.
- Multiple security groups can be associated with a network interface.

## 15. Network ACL (NACL)

A Network ACL is a firewall that operates at the subnet level.

It controls inbound and outbound traffic entering or leaving a subnet.

### Important Characteristics

- Network ACLs are stateless.
- They support both allow and deny rules.
- Rules are evaluated in numerical order.
- The first matching rule is applied.
- Every subnet is associated with a network ACL.

### Security Group vs Network ACL

| Security Group | Network ACL |
|---|---|
| Operates at network interface level | Operates at subnet level |
| Stateful | Stateless |
| Allow rules only | Allow and deny rules |
| Rules are not evaluated by numerical order | Rules are evaluated in numerical order |
| Return traffic is automatically allowed | Return traffic must be explicitly allowed |

---

# Part 7: Complete Real-World VPC Architecture

## 16. Deploying an E-commerce Application

Imagine you are building an e-commerce application using:

- Next.js frontend
- Node.js backend
- MySQL database

You want to deploy it securely on AWS.

A possible architecture is:

### VPC Configuration

VPC CIDR:

`10.0.0.0/16`

### Subnet Configuration

| Subnet | CIDR | Availability Zone | Purpose |
|---|---|---|---|
| Public Subnet A | 10.0.1.0/24 | AZ-1 | Load Balancer |
| Public Subnet B | 10.0.2.0/24 | AZ-2 | Load Balancer |
| Private Subnet A | 10.0.11.0/24 | AZ-1 | Backend EC2 |
| Private Subnet B | 10.0.12.0/24 | AZ-2 | Backend EC2 |
| Database Subnet A | 10.0.21.0/24 | AZ-1 | MySQL |
| Database Subnet B | 10.0.22.0/24 | AZ-2 | MySQL |

### Architecture Explanation

**1. Public Subnets**

The Application Load Balancer is deployed across public subnets.

Customers access the application through the load balancer.

**2. Private Subnets**

Backend EC2 instances run in private subnets.

The load balancer forwards customer requests to these instances.

**3. Database Subnets**

The MySQL database runs in private subnets.

Only authorised application servers can connect to the database.

**4. NAT Gateway**

Backend instances can use a NAT Gateway to initiate outbound internet connections when required.

**5. Security Groups**

You can configure:

- Load balancer security group: Allows HTTP and HTTPS from customers.
- Backend security group: Allows application traffic only from the load balancer security group.
- Database security group: Allows MySQL traffic on port 3306 only from the backend security group.

### Why Is This Architecture Secure?

Because:

- The database is not directly exposed to the internet.
- Backend servers do not need public IP addresses.
- Customers communicate through the load balancer.
- Security groups restrict communication between application layers.
- Multiple Availability Zones improve resilience.

---

# Part 8: Important Additional Concepts

## 17. Default VPC

When you create an AWS account, AWS generally provides a default VPC in each Region where the default VPC is available.

A default VPC normally includes:

- A VPC.
- Public subnets in the Region's Availability Zones.
- An Internet Gateway.
- Route tables.
- Default security group.
- Network ACL.

It allows beginners to launch EC2 instances without manually designing a network first.

## 18. DHCP Options Set

DHCP stands for Dynamic Host Configuration Protocol.

A DHCP options set provides network configuration information to instances in a VPC.

For example:

- Domain name.
- DNS servers.
- NTP servers.

AWS provides a default DHCP options set for a VPC.

## 19. DNS in VPC

DNS stands for Domain Name System.

It translates domain names into IP addresses.

For example:

When you visit `google.com`, DNS helps your device find the corresponding IP address.

Two important VPC settings are:

- DNS resolution: Allows instances to use DNS resolution through Amazon-provided DNS.
- DNS hostnames: Enables public DNS hostnames for instances with public IPv4 addresses, where applicable.

## 20. VPC Peering

VPC Peering allows two VPCs to communicate privately using their private IP addresses.

Example:

- VPC A contains your frontend application.
- VPC B contains an internal service.

You can establish VPC Peering to allow communication between them.

The VPC CIDR ranges must not overlap.

You must also configure appropriate routes and security rules.

---

# Part 9: Important Differences to Memorise

## 21. VPC vs Subnet

| VPC | Subnet |
|---|---|
| A virtual network | A smaller network inside a VPC |
| Exists within a Region | Exists within one Availability Zone |
| Contains subnets | Contains network interfaces and resources |
| Has an IPv4 CIDR range | Has its own CIDR range within the VPC |

## 22. Internet Gateway vs NAT Gateway

| Internet Gateway | NAT Gateway |
|---|---|
| Enables internet connectivity for a VPC | Enables private resources to initiate outbound internet connections |
| Used by public subnets | Commonly used by private subnets |
| Does not require an Elastic IP | Public NAT Gateway requires an Elastic IP |
| Supports direct internet connectivity when other requirements are met | Does not accept unsolicited inbound internet connections |

## 23. Public vs Private IP

| Public IP | Private IP |
|---|---|
| Used for public internet communication | Used for private network communication |
| Must be globally unique at a given time | Can be reused in different private networks |
| Can be reached over the internet if security and routing permit | Not directly routable over the public internet |

---

# Part 10: Important Interview Questions

### Q1. What is AWS VPC?

AWS VPC is a logically isolated virtual network where you can launch AWS resources and control their networking configuration.

### Q2. What is a subnet?

A subnet is a smaller IP network inside a VPC. It allows you to organise resources and control their network connectivity.

### Q3. What is the difference between a public and private subnet?

A public subnet has a route to an Internet Gateway, whereas a private subnet does not have a direct route to an Internet Gateway.

### Q4. Can a VPC contain multiple subnets?

Yes. A VPC can contain multiple subnets across different Availability Zones.

### Q5. Can a subnet belong to multiple Availability Zones?

No. Each subnet belongs to exactly one Availability Zone.

### Q6. What is an Internet Gateway?

An Internet Gateway enables communication between a VPC and the internet.

### Q7. What is a NAT Gateway?

A NAT Gateway allows resources in private subnets to initiate connections to the internet without allowing unsolicited inbound internet connections.

### Q8. What is a route table?

A route table determines where network traffic should be directed.

### Q9. What is the difference between a security group and a Network ACL?

A security group operates at the network interface level and is stateful. A Network ACL operates at the subnet level and is stateless.

### Q10. What is CIDR?

CIDR is a method of representing IP address ranges using an IP address and a prefix length.

---

# Part 11: Final Summary

| Concept | Simple Meaning |
|---|---|
| Network | Connected devices that communicate |
| IP Address | Address used to identify a network interface |
| CIDR | Represents an IP address range |
| VPC | Your isolated virtual network in AWS |
| Subnet | A smaller network inside a VPC |
| Public Subnet | Subnet with a route to an Internet Gateway |
| Private Subnet | Subnet without a direct route to an Internet Gateway |
| Internet Gateway | Enables internet connectivity |
| NAT Gateway | Allows private resources to initiate outbound internet connections |
| Route Table | Determines where network traffic goes |
| Security Group | Stateful firewall for network interfaces |
| Network ACL | Stateless firewall for subnets |
| Availability Zone | Isolated location within an AWS Region |
| VPC Peering | Private connectivity between two VPCs |

## The Most Important Things to Remember

1. A VPC is your virtual network.
2. A subnet is a smaller network inside your VPC.
3. Every subnet belongs to one Availability Zone.
4. A public subnet has a route to an Internet Gateway.
5. A private subnet has no direct route to an Internet Gateway.
6. A NAT Gateway allows private resources to initiate outbound internet connections.
7. Route tables control network traffic.
8. Security groups protect network interfaces.
9. Network ACLs protect subnets.
10. CIDR determines the size of your network.

**My recommendation:** Do not memorise these concepts separately. Understand how an internet request travels from a customer to your load balancer, backend server, and database. That will make AWS networking much easier to understand.
