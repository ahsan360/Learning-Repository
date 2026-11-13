
# 7-1 Purpose-Built Databases on AWS
# 7-2 Choosing the Right Database

## 1. What is a Database?

A database is an organised system used to store, manage, retrieve, and update data.

Examples:
- User information
- Product details
- Orders
- Payments
- Customer records

## 2. What is a DBMS?

DBMS stands for Database Management System.

It is software used to create, manage, and interact with databases.

Examples:
- MySQL
- PostgreSQL
- MongoDB
- Redis
- Cassandra

## 3. What are Purpose-Built Databases?

A purpose-built database is designed and optimised for a specific type of workload or data model.

Instead of using one database for every application requirement, we select a database that is best suited to a particular task.

### Why do we need purpose-built databases?

Different applications have different requirements.

| Requirement | Suitable Database |
|---|---|
| Financial transactions | Relational |
| Flexible JSON documents | Document |
| Fast key-value access | Key-value |
| Caching | In-memory |
| Complex relationships | Graph |
| Time-based data | Time-series |
| Large-scale analytics | Data warehouse |

---

# 4. AWS Purpose-Built Database Services

## 4.1 Amazon RDS (Relational Database Service)

**What is it?**

Amazon RDS is a managed relational database service that allows users to run relational database engines on AWS.

**Database type:** Relational

**Supported database engines:**
- MySQL
- PostgreSQL
- MariaDB
- Oracle
- Microsoft SQL Server
- IBM Db2

**When to use it:**
- Banking applications
- E-commerce applications
- Financial transactions
- Applications requiring SQL queries
- Applications requiring relational data

**Key features:**
- Automated backups
- Database monitoring
- Managed maintenance
- Multi-AZ deployment options
- Read replicas for supported engines

## 4.2 Amazon Aurora

**What is it?**

Amazon Aurora is an AWS-developed relational database engine compatible with MySQL and PostgreSQL.

It is designed for high performance, availability, and scalability.

**Database type:** Relational

**When to use it:**
- High-performance relational applications
- Enterprise applications
- Applications requiring high availability
- Applications with demanding database workloads

**Key features:**
- MySQL and PostgreSQL compatibility
- Distributed storage architecture
- Automated backups
- High availability
- Aurora Serverless options

**RDS vs Aurora:**

| Amazon RDS | Amazon Aurora |
|---|---|
| Managed relational database service | AWS-developed relational database engine |
| Supports multiple database engines | MySQL and PostgreSQL compatible |
| General-purpose relational workloads | High-performance relational workloads |

## 4.3 Amazon DynamoDB

**What is it?**

Amazon DynamoDB is a fully managed, serverless NoSQL database service.

It supports key-value and document data models.

**Database type:** NoSQL

**When to use it:**
- Shopping carts
- Gaming applications
- User sessions
- User preferences
- High-traffic applications
- Applications requiring low-latency key-based access

**Key features:**
- Serverless architecture
- Automatic scaling options
- High availability
- Low-latency data access
- Automatic data replication across multiple Availability Zones
- On-demand and provisioned capacity modes

**Important concepts:**
- Table: Collection of items.
- Item: Individual record.
- Attribute: Property of an item.
- Partition key: Determines the logical partition for an item.
- Sort key: Organises items within a partition key.

## 4.4 Amazon DocumentDB

**What is it?**

Amazon DocumentDB is a managed document database service that provides MongoDB compatibility.

**Database type:** Document database

**When to use it:**
- Content management systems
- Product catalogues
- User profiles
- Applications using MongoDB-compatible drivers and APIs
- Applications requiring flexible JSON-like documents

**Key features:**
- Managed database infrastructure
- Document-based data model
- MongoDB compatibility
- Automatic backups
- Storage scaling

**Important:**
DocumentDB is not identical to MongoDB. Some MongoDB features and behaviours may not be supported.

## 4.5 Amazon ElastiCache

**What is it?**

Amazon ElastiCache is a managed in-memory caching service.

It supports Redis OSS and Memcached.

**Database type:** In-memory database / caching

**When to use it:**
- Application caching
- Session management
- Frequently accessed data
- Real-time applications
- Gaming leaderboards
- Reducing database workload

**Key features:**
- Very fast data access
- In-memory storage
- Managed caching infrastructure
- Reduced database load
- Support for Redis OSS and Memcached

**Important:**
Caching stores frequently accessed data temporarily to reduce repeated database queries.

## 4.6 Amazon Neptune

**What is it?**

Amazon Neptune is a fully managed graph database service designed to store and query highly connected data.

**Database type:** Graph database

**When to use it:**
- Social networks
- Fraud detection
- Recommendation engines
- Knowledge graphs
- Relationship analysis

**Key concepts:**
- Node: Represents an entity.
- Edge: Represents a relationship.
- Property: Describes an entity or relationship.

## 4.7 Amazon Keyspaces

**What is it?**

Amazon Keyspaces is a managed, Apache Cassandra-compatible wide-column database service.

**Database type:** Wide-column NoSQL

**When to use it:**
- IoT applications
- Large-scale distributed workloads
- Vehicle tracking
- Applications already using Apache Cassandra

**Key features:**
- Serverless
- Managed infrastructure
- Cassandra compatibility
- Automatic scaling options

## 4.8 Amazon Timestream

**What is it?**

Amazon Timestream is a purpose-built time-series database service.

It is designed to store and analyse time-stamped data.

**Database type:** Time-series database

**When to use it:**
- IoT sensor data
- Server monitoring
- Application metrics
- Industrial equipment monitoring
- Temperature tracking

**Example:**

| Timestamp | Temperature |
|---|---|
| 10:00 | 25°C |
| 10:01 | 26°C |
| 10:02 | 27°C |

## 4.9 Amazon Redshift

**What is it?**

Amazon Redshift is a managed cloud data warehouse service designed for large-scale data analytics.

**Database type:** Data warehouse

**When to use it:**
- Business intelligence
- Historical sales analysis
- Data analytics
- Reporting
- Large-scale analytical queries

**Key features:**
- Columnar storage
- Massively parallel processing (MPP)
- SQL-based analytics
- Integration with business intelligence tools
- Integration with other AWS data services

---

# 5. Choosing the Right Database

Choosing the right database depends on:

1. Data structure
2. Query patterns
3. Performance requirements
4. Scalability
5. Availability
6. Consistency requirements
7. Cost
8. Operational complexity

## 5.1 Database Selection Table

| Requirement | AWS Service |
|---|---|
| Relational database with SQL | Amazon RDS |
| High-performance relational database | Amazon Aurora |
| Serverless NoSQL database | Amazon DynamoDB |
| MongoDB-compatible document database | Amazon DocumentDB |
| In-memory caching | Amazon ElastiCache |
| Graph relationships | Amazon Neptune |
| Cassandra-compatible database | Amazon Keyspaces |
| Time-series data | Amazon Timestream |
| Data warehouse and analytics | Amazon Redshift |

## 5.2 OLTP vs OLAP

### OLTP (Online Transaction Processing)

OLTP systems handle everyday application transactions.

Examples:
- Bank deposits
- Money transfers
- Customer orders
- Payment processing
- Inventory updates

Suitable services:
- Amazon RDS
- Amazon Aurora
- Amazon DynamoDB (for suitable NoSQL transaction workloads)

### OLAP (Online Analytical Processing)

OLAP systems analyse large volumes of historical data.

Examples:
- Annual sales reports
- Business intelligence
- Revenue analysis
- Customer behaviour analysis

Suitable service:
- Amazon Redshift

| OLTP | OLAP |
|---|---|
| Handles transactions | Analyses data |
| Frequent reads and writes | Complex analytical queries |
| Operational workloads | Analytical workloads |
| RDS / Aurora | Redshift |

## 5.3 Relational vs NoSQL

| Relational Database | NoSQL Database |
|---|---|
| Structured tables | Flexible data models |
| Rows and columns | Documents, key-value, graph, etc. |
| SQL queries | Database-specific query methods |
| Relationships and JOINs | Often uses denormalised data |
| Defined schemas | Often flexible schemas |
| RDS / Aurora | DynamoDB / DocumentDB |

## 5.4 Caching vs Primary Database

**Primary Database:**
- Stores the main application data.
- Provides persistent data storage.
- Used as the main source of truth.

**Cache:**
- Stores frequently accessed data.
- Provides faster data retrieval.
- Reduces repeated database queries.
- Often stores temporary copies of data.

AWS service: Amazon ElastiCache.

---

# 6. Important AWS Exam Scenarios

| Exam Scenario | Correct Answer |
|---|---|
| Need a managed MySQL database | Amazon RDS |
| Need high-performance MySQL compatibility | Amazon Aurora |
| Need a serverless NoSQL database | Amazon DynamoDB |
| Need MongoDB compatibility | Amazon DocumentDB |
| Need in-memory caching | Amazon ElastiCache |
| Need graph-based relationships | Amazon Neptune |
| Need Cassandra compatibility | Amazon Keyspaces |
| Need time-series data storage | Amazon Timestream |
| Need a cloud data warehouse | Amazon Redshift |
| Need to reduce repeated database queries | Amazon ElastiCache |
| Need business intelligence and historical analytics | Amazon Redshift |
| Need to analyse relationships between people | Amazon Neptune |

---

# 7. Quick Revision Notes

Memorise these associations:

- RDS = Relational database
- Aurora = High-performance relational database
- DynamoDB = Serverless NoSQL
- DocumentDB = MongoDB-compatible document database
- ElastiCache = In-memory caching
- Neptune = Graph database
- Keyspaces = Cassandra-compatible wide-column database
- Timestream = Time-series database
- Redshift = Data warehouse

## 8. Important Exam Tips

1. Do not confuse RDS with Aurora.
2. Do not confuse DynamoDB with DocumentDB.
3. Remember that ElastiCache is designed for caching.
4. Remember that Neptune is designed for connected data.
5. Remember that Redshift is for analytics, not ordinary transactional workloads.
6. Understand the difference between OLTP and OLAP.
7. Pay attention to keywords such as serverless, relational, graph, caching, analytics, and time-series.

**Exam strategy:** Focus on identifying the correct AWS service from the requirements described in a scenario.
