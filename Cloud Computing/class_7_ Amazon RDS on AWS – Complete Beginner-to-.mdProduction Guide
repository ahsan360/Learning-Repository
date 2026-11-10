# Amazon RDS on AWS – Complete Beginner-to-Production Guide

## 1. What Is a Database?

A database is an organised system for storing, managing, retrieving, and updating information.

For example, an e-commerce application needs to store:

- Users
- Products
- Orders
- Payments
- Customer addresses

A database stores this information so that applications can access it whenever necessary.

### Example: Users Table

| id | name | email |
|---|---|---|
| 1 | Ahsan | ahsan@gmail.com |
| 2 | Rahim | rahim@gmail.com |
| 3 | Karim | karim@gmail.com |

## 2. What Is Amazon RDS?

Amazon RDS (Relational Database Service) is a managed relational database service provided by AWS.

It allows developers to create, operate, and manage relational databases without manually managing all the underlying infrastructure.

### Without Amazon RDS

If you want to host MySQL on an EC2 instance, you need to:

1. Create an EC2 instance.
2. Install Ubuntu or Amazon Linux.
3. Install MySQL.
4. Configure MySQL.
5. Create database users.
6. Configure database security.
7. Configure automated backups.
8. Monitor database performance.
9. Manage database updates.
10. Handle database maintenance.

### With Amazon RDS

AWS manages many of these responsibilities for you.

You mainly need to:

1. Select a database engine.
2. Configure computing resources.
3. Configure storage.
4. Configure networking.
5. Set up database credentials.
6. Create the database.

**Important:** Amazon RDS is a managed database service, not a database engine itself.

---

## 3. Database Engines Supported by RDS

A database engine is the software responsible for storing, managing, and querying information.

Amazon RDS supports several database engines.

| Database Engine | Description |
|---|---|
| MySQL | Popular open-source relational database |
| PostgreSQL | Advanced open-source relational database |
| MariaDB | Open-source database derived from MySQL |
| Oracle | Enterprise relational database |
| Microsoft SQL Server | Microsoft's relational database |
| IBM Db2 | Enterprise relational database |

### Which One Should You Learn?

Start with MySQL because it is widely used in backend development.

You can later learn PostgreSQL and explore other database engines.

---

## 4. Amazon RDS Architecture

Consider an application with a frontend, backend and database.

```text
                 USER
                   |
                   v
                FRONTEND
                   |
                   v
               BACKEND API
                 (EC2)
                   |
                   | MySQL Connection
                   | Port 3306
                   |
                   v
               AMAZON RDS
                  MySQL
                   |
                   v
                DATABASE
```

### How Does It Work?

1. A user sends a request to the frontend.
2. The frontend communicates with the backend API.
3. The backend connects to Amazon RDS.
4. RDS executes the SQL query.
5. RDS returns the result to the backend.
6. The backend sends a response to the user.

**Remember:**

- EC2 runs your backend application.
- RDS manages your relational database.
- VPC provides the networking environment.
- Security groups control network access.

---

## 5. Important Amazon RDS Terminology

### 5.1 DB Instance

A DB instance is the computing environment where your database engine runs.

For example, when you create an RDS MySQL instance, AWS provisions the required infrastructure and runs MySQL for you.

Think of it as a database server managed by AWS.

### 5.2 DB Instance Class

An instance class determines the computing capacity available to your database.

It includes:

- CPU
- RAM
- Network performance

Examples:

| Instance Class | Purpose |
|---|---|
| db.t3.micro | Small workloads |
| db.t4g.micro | Small workloads |
| db.t3.small | Small applications |
| db.m series | General-purpose workloads |
| db.r series | Memory-intensive workloads |

A larger instance generally costs more.

Availability depends on the selected database engine and AWS region.

### 5.3 Database Storage

Storage is where your database files and records are stored.

Common RDS storage types:

- General Purpose SSD (gp3)
- General Purpose SSD (gp2)
- Provisioned IOPS SSD (io1/io2)

For beginners, General Purpose SSD is a sensible choice.

**Important:** Computing resources and database storage are separate resources.

### 5.4 Database Endpoint

An endpoint is the network address used by applications to connect to an RDS database.

Example:

```text
mydatabase.abc123xyz.us-east-1.rds.amazonaws.com
```

Your backend uses this endpoint to communicate with RDS.

Example:

```javascript
const connection = mysql.createConnection({
  host: process.env.DB_HOST,
  user: process.env.DB_USER,
  password: process.env.DB_PASSWORD,
  database: process.env.DB_NAME,
  port: 3306
});
```

### 5.5 Database Port

Different database engines use different default ports.

| Database Engine | Default Port |
|---|---:|
| MySQL | 3306 |
| PostgreSQL | 5432 |
| MariaDB | 3306 |
| SQL Server | 1433 |
| Oracle | 1521 |
| IBM Db2 | 50000 |

### 5.6 VPC (Virtual Private Cloud)

A VPC is a logically isolated network inside AWS.

Your RDS database is deployed inside a VPC.

A VPC allows you to control how AWS resources communicate with each other.

### 5.7 Security Group

A security group acts as a virtual firewall.

It controls inbound and outbound network traffic.

Example:

```text
Type: MySQL/Aurora
Protocol: TCP
Port: 3306
Source: EC2 Security Group
```

This allows your EC2 application to connect to the RDS database.

Never allow unrestricted internet access to a production database.

---

## 6. Public vs Private RDS

### 6.1 Publicly Accessible Database

A publicly accessible RDS database can receive connections through a public network address.

Characteristics:

- Can be accessed from your computer if network rules permit it.
- Requires a public network route.
- Requires appropriate security group rules.
- Useful for controlled development and testing.

For learning, you can enable public accessibility and restrict access to your current public IP address.

### 6.2 Privately Accessible Database

A private RDS database does not have direct public internet accessibility.

Characteristics:

- Your EC2 application can connect through the VPC.
- The database is not directly exposed to the internet.
- Suitable for production applications.
- External developers need a secure access method such as VPN or a bastion host.

### Recommended Configuration

For learning:

```text
Public Accessibility: Yes
Security Group Source: My Current IP
```

For production:

```text
Public Accessibility: No
Security Group Source: Backend EC2 Security Group
```

---

# 7. Creating Your First Amazon RDS Database

We will create a MySQL database using the AWS Management Console.

### Step 1: Open Amazon RDS

1. Log in to your AWS account.
2. Search for RDS.
3. Open Amazon RDS.
4. Select Databases.
5. Click Create database.

### Step 2: Select Creation Method

You will see two options:

- Easy create
- Standard create

Choose Standard create.

This gives you greater control over the configuration.

### Step 3: Select Database Engine

Choose:

```text
Engine Type: MySQL
```

Select a supported MySQL version.

### Step 4: Select a Template

Available templates may include:

- Production
- Dev/Test
- Free tier

For learning, select an eligible Free Tier template if available.

Avoid production configurations for this exercise.

### Step 5: Configure Database Credentials

Example:

```text
DB Instance Identifier: my-first-database
Master Username: dbadmin
Credentials Management: Self-managed
Master Password: Your Strong Password
```

The master username is the administrative database user.

It has extensive database privileges.

For production, create separate application users with restricted permissions.

### Step 6: Configure Instance Class

Choose an eligible small instance.

For example:

```text
db.t3.micro
```

Alternatively, use an eligible db.t4g.micro if available.

### Step 7: Configure Storage

Example:

```text
Storage Type: General Purpose SSD
Allocated Storage: 20 GiB (if supported)
```

Avoid enabling storage autoscaling without understanding its cost implications.

### Step 8: Configure Connectivity

Example:

```text
VPC: Default VPC
Public Access: Yes (learning only)
VPC Security Group: Create New
Security Group Name: rds-mysql-learning-sg
```

Configure the inbound rule:

```text
Type: MySQL/Aurora
Protocol: TCP
Port: 3306
Source: My Current IP
```

Do not use 0.0.0.0/0.

### Step 9: Additional Configuration

Example:

```text
Initial Database Name: learning_db
Automated Backups: Enabled
Backup Retention: 1 Day (if available)
Encryption: Enabled
```

The initial database name is different from the DB instance identifier.

### Step 10: Create Database

Click Create Database.

The status will initially show:

```text
Creating
```

After provisioning is complete:

```text
Available
```

The database may take several minutes to become available.

---

# 8. Connecting to Amazon RDS

You can connect to RDS using:

1. MySQL Workbench
2. MySQL Command Line
3. Node.js
4. EC2
5. Other database management tools

## Method 1: MySQL Workbench

Download:

https://dev.mysql.com/downloads/workbench/

After installation:

1. Open MySQL Workbench.
2. Click the + icon beside MySQL Connections.
3. Configure the connection.

Example:

| Field | Value |
|---|---|
| Connection Name | AWS RDS |
| Hostname | Your RDS Endpoint |
| Port | 3306 |
| Username | dbadmin |
| Password | Your RDS Password |

Click Test Connection.

If successful, you can manage your database using MySQL Workbench.

### Common Connection Problems

Check these items if the connection fails:

- Is the RDS status Available?
- Is public access enabled for your learning setup?
- Does the security group allow your current IP?
- Is the port 3306?
- Is the endpoint correct?
- Are the username and password correct?
- Is the database in the expected VPC and subnet configuration?

---

# 9. Connecting RDS to Node.js

As a backend developer, you should know how to connect RDS to your application.

### Step 1: Install MySQL Package

```bash
npm install mysql2
```

### Step 2: Create database.js

```javascript
const mysql = require("mysql2/promise");

const pool = mysql.createPool({
  host: process.env.DB_HOST,
  user: process.env.DB_USER,
  password: process.env.DB_PASSWORD,
  database: process.env.DB_NAME,
  port: 3306,

  waitForConnections: true,
  connectionLimit: 10,
  queueLimit: 0
});

module.exports = pool;
```

### Step 3: Configure Environment Variables

Create a `.env` file.

```env
DB_HOST=your-rds-endpoint
DB_USER=dbadmin
DB_PASSWORD=your-password
DB_NAME=learning_db
```

Never commit your `.env` file to GitHub.

### Step 4: Test the Database Connection

```javascript
const db = require("./database");

async function testDatabase() {
  try {
    const [rows] = await db.query(
      "SELECT NOW() AS current_time"
    );

    console.log(rows);
  } catch (error) {
    console.error(error);
  }
}

testDatabase();
```

If successful, the database server will return its current time.

### Important Production Advice

For production:

- Keep RDS private.
- Connect through your backend inside the VPC.
- Use Secrets Manager for database credentials.
- Use connection pooling.
- Avoid hardcoding passwords.
- Configure TLS encryption for database connections.

---

# 10. How EC2 Communicates with RDS

Suppose you have:

- EC2 running your Node.js application.
- RDS running MySQL.
- Both resources inside the same VPC.

Architecture:

```text
                 INTERNET
                    |
                    v
              EC2 INSTANCE
              Backend API
                    |
                    |
               TCP 3306
                    |
                    v
                AMAZON RDS
                  MySQL
```

### Configure EC2 Security Group

Example:

```text
Security Group Name: backend-sg
```

### Configure RDS Security Group

Example:

```text
Security Group Name: database-sg
```

Inbound rule:

```text
Type: MySQL/Aurora
Protocol: TCP
Port: 3306
Source: backend-sg
```

This allows resources associated with the backend security group to connect to RDS.

You do not need to expose the database to the entire internet.

---

# 11. Important Amazon RDS Features

## 11.1 Automated Backups

Automated backups allow you to recover your database after accidental deletion of records or other failures.

RDS supports:

- Automated backups
- Point-in-time recovery
- Manual snapshots

### Automated Backup

AWS automatically backs up your database according to your configured retention period.

You can restore the database to a supported point in time within the backup retention window.

### Manual Snapshot

You manually create a snapshot at a particular moment.

Example:

```text
Database: production-db

Snapshot:
production-db-backup-2026-11-10
```

You can restore a database from the snapshot later.

## 11.2 Multi-AZ Deployment

Multi-AZ improves database availability.

Example:

```text
        Availability Zone A
          Primary Database
                 |
                 |
         Synchronous Replication
                 |
                 |
        Availability Zone B
          Standby Database
```

If the primary database experiences a failure, RDS can automatically fail over to the standby.

### Important Difference

- Single-AZ: One primary deployment.
- Multi-AZ: Additional standby infrastructure for higher availability.

Multi-AZ generally costs more.

## 11.3 Read Replicas

Read replicas help distribute read-heavy workloads.

Suppose your application has 100,000 users.

Most users are reading data, while fewer users are updating it.

Your primary database may experience heavy read traffic.

Architecture:

```text
               APPLICATION
                    |
                    v
             PRIMARY DATABASE
                /       \
               /         \
              v           v
        READ REPLICA  READ REPLICA
```

Your application can distribute SELECT queries to read replicas when appropriate.

Write queries generally go to the primary database.

### Important Difference

| Feature | Multi-AZ | Read Replica |
|---|---|---|
| Primary Purpose | High availability | Read scalability |
| Main Use | Failover | Distribute read traffic |
| Standby | Yes, depending on deployment type | No, it serves read workloads |
| Read Workloads | Not its main purpose | Yes |

Read replicas may experience replication lag.

---

# 12. Amazon RDS Pricing

Amazon RDS is not automatically free.

You may be charged for several components.

| Component | Billing Explanation |
|---|---|
| DB Instance | Computing resources per running hour |
| Storage | Allocated database storage |
| Backups | Applicable backup storage charges |
| Data Transfer | Applicable network transfer charges |
| Public IPv4 | Applicable public IPv4 charges |
| Multi-AZ | Additional database infrastructure |
| Read Replicas | Additional database resources |

### Your AWS Credits

You have $100 in AWS credits.

Use them carefully.

Recommended learning configuration:

```text
Database Engine: MySQL
Deployment: Single-AZ
Instance: Eligible Small Instance
Storage: Small General Purpose SSD
Public Access: Yes, restricted to your IP
Backups: Minimal retention
```

Always check your account's Free Tier eligibility and current pricing.

Useful resources:

- RDS Pricing: https://aws.amazon.com/rds/pricing/
- AWS Billing: https://console.aws.amazon.com/billing/home
- AWS Pricing Calculator: https://calculator.aws/

### Stopping an RDS Instance

When you stop an RDS instance:

- Database compute charges stop temporarily.
- Storage charges continue.
- Some other applicable charges may continue.
- RDS automatically restarts a stopped DB instance after seven days.

### Deleting an RDS Instance

When you delete an RDS instance:

- The DB instance is removed.
- You can choose whether to create a final snapshot.
- Retained snapshots may continue to incur charges.
- Other retained resources may also incur charges.

Always inspect snapshots and backups before deletion.

---

# 13. Production-Level RDS Knowledge

To work with RDS in production, learn these concepts:

| Topic | What to Learn |
|---|---|
| Database Engines | MySQL, PostgreSQL |
| DB Instances | Instance classes, CPU, RAM |
| Storage | gp3, IOPS, storage autoscaling |
| Networking | VPC, subnets, DB subnet groups |
| Security | Security groups, IAM authentication |
| Credentials | AWS Secrets Manager |
| Backups | Automated backups, snapshots |
| Availability | Multi-AZ, failover |
| Scalability | Read replicas |
| Monitoring | CloudWatch |
| Performance | Slow queries, indexes |
| Maintenance | Engine upgrades, maintenance windows |
| Disaster Recovery | Point-in-time recovery |
| Connection Management | Connection pooling, RDS Proxy |

---

# 14. Practical Learning Assignment

Complete these exercises in order.

- [ ] Open Amazon RDS in the AWS Console.
- [ ] Create a MySQL DB instance.
- [ ] Configure a security group allowing only your IP.
- [ ] Connect using MySQL Workbench.
- [ ] Create a users table.
- [ ] Insert three sample users.
- [ ] Retrieve users using SELECT.
- [ ] Connect your Node.js application to RDS.
- [ ] Create a manual database snapshot.
- [ ] Delete the learning DB instance.
- [ ] Inspect remaining resources and billing.

### SQL Practice

Create a users table:

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Insert sample records:

```sql
INSERT INTO users (name, email)
VALUES
('Ahsan', 'ahsan@gmail.com'),
('Rahim', 'rahim@gmail.com'),
('Karim', 'karim@gmail.com');
```

Retrieve records:

```sql
SELECT * FROM users;
```

Update a record:

```sql
UPDATE users
SET name = 'Ahsan Habib'
WHERE id = 1;
```

Delete a record:

```sql
DELETE FROM users
WHERE id = 3;
```

---

# 15. AWS RDS Learning Roadmap

Follow this sequence to progress from beginner to production-level knowledge.

### Level 1: Fundamentals

- What is a relational database?
- What is Amazon RDS?
- Database engines
- DB instances
- Instance classes
- Storage types
- Database endpoints
- Database ports

### Level 2: Networking

- VPC
- Public and private subnets
- DB subnet groups
- Security groups
- Internet Gateway
- NAT Gateway
- EC2-to-RDS connectivity

### Level 3: Database Connectivity

- MySQL Workbench
- MySQL CLI
- Node.js integration
- Connection pooling
- Environment variables

### Level 4: Database Security

- Master user
- Application database users
- Least privilege
- Security groups
- IAM database authentication
- AWS Secrets Manager
- Encryption at rest
- Encryption in transit

### Level 5: Backup and Recovery

- Automated backups
- Manual snapshots
- Point-in-time recovery
- Database restoration
- Disaster recovery planning

### Level 6: Availability and Scalability

- Multi-AZ
- Automatic failover
- Read replicas
- RDS Proxy
- Database scaling

### Level 7: Production Monitoring

- CloudWatch
- CPU utilisation
- Free storage space
- Database connections
- Read and write latency
- Slow query analysis
- Performance optimisation
- Maintenance and upgrades

---

# 16. Recommended Official AWS Resources

1. Amazon RDS Documentation:
   https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html

2. Creating an RDS DB Instance:
   https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CreateDBInstance.html

3. RDS Pricing:
   https://aws.amazon.com/rds/pricing/

4. RDS Backups:
   https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithAutomatedBackups.html

5. RDS Multi-AZ:
   https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html

6. RDS Read Replicas:
   https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html

---

# 17. Final Recommendations

Do not rush into production configurations.

Start with a small MySQL RDS instance and connect it to your local Node.js application.

After understanding the basic connection process:

1. Learn VPC and subnet configuration.
2. Connect EC2 to private RDS.
3. Configure security groups properly.
4. Implement database backups.
5. Practise database restoration.
6. Learn Multi-AZ and read replicas.
7. Implement monitoring and performance optimisation.

**Your ultimate goal:** Be able to design, deploy, secure, monitor, back up, and troubleshoot an AWS-hosted relational database in a real production environment.
