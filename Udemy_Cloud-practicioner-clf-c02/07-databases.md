# Databases

- Store data in a database allows you to structure your data, build indexes to efficiently query / search through the data.
- Define relationships between datasets
- Relational databases - looks like Excel, having links between each table
- you can use SQL Language to perform queries / lookups
- NoSQL Databases - non relational databases
- specific purpose for specific data models and have flexible schemas
- benefits: flexibility, easy to evolve data model
- high-performance - optimized for a specific data model
- scalability - designed to scale out by using distributed clusters
- highly funcional - types optimized for the data model

## Shared Responsibility

- AWS offers manage different databases
- Benefits include:
  - quick provisioning, high availability and horizontal scaling
  - Automated Backup and restore, Operations, Upgrades
  - Operating system Patching is handled by AWS
  - Monitoring and alerting
- many databases technologies could be run on EC2, but you must handle yourself the resiliency, backup, patching, high availability, fault tolerance, scalability

## RDS

- Relational Database Service
- managed DB Service for DB use SQL as a query language
- allows you to create databases in the cloud that are managed by AWS

  - Postgres
  - MySQL
  - Oracle
  - MariaDB
  - Microsoft SQL Server
  - IBM DB2
  - Aurora (AWS Proprietary Database)

- Advantages over EC2:
  - RDS is a managed service
  - Continuos backup and restore to specific timestamp
  - monitoring dashboard
  - multi AZ setup for DR Disaster Recovery
  - Maintenance windows for upgrades
  - Scaling capability (vertical and horizontal)
  - Storage backed by EBS
  - but you can't ssh into your instances
  - Allows you to create snapshots and restore it in another region or account

### RDS Solution Architecture

- Elastic Load Balances -> EC2 Instances (Auto scaling maybe) -> save the data in the SQL Database
- Classic solution architecture

### Amazon Aurora

- Proprietary technology from AWS (not open source)
- PostgreSQL and MySQL are both supported as Aurora DB
- Aurora is AWS cloud optimized and claims 5x performance improvement over MySQL on RDS, over 3 times performance of Postgres on RDS
- Aurora costs more than RDS, but is more efficient, so should be more cost effective
- Aurora is not free tier, RDS is included
- **Aurora Serverless** -> Automate database instantiation and auto-scaling based on actual usage
  - Postgres and MySQL are both supported
  - Least management overhead
  - pay per second, can be more cost effective
  - good for infrequent, intermittent or unpredictable workloads

### RDS Deployments

#### Read Replica

- you can create replicas that allow your application to read from
- until 15 read replicas
- Writing data is always done in the main database

#### Multi AZ

- Failover in case of AZ outage (high availability)
- Replication across AZ (Failover DB)
- Data is only read/written in the main database
- Only one other AZ as failover

#### Multi Region

- E.g: main in the eu-west-1 -> have a read replica in us-east-2
- Disaster recovery in case of region issue
- local performance for global reads
- replication cost

## Elasticache

- Managed Redis or Memcached
- caches are in-memory databases with high performance, low latency
- reduce load off databases for read intensive workloads
- AWS takes care of OS Maintenance and patching, Backups, setup, optimizations, configuration, monitoring, failure recovery
- Elastic Load Balancer -> EC2 -> Read from AWS RDS with caching in ElastiCache (in memory database)

## DynamoDB

- Fully managed Highly Available with replication across 3 AZs
- **NoSQL Database** - not a relational database
- Scales to massive workloads, distributed "serverless" database
- Millions of requests per seconds, trillions of rows, 100s of TB storage
- Fast and consistent in performance
- **Single-digit millisecond latency -- low latency retrieval**
- Integrated with IAM for security, authorization and administration
- Low cost and auto scaling capabilities
- Standard & Infrequent Access Table Class
- Key/value database: Primary key with partition key and sort key
- One single "table", no joining

### DynamoDB Accelerator - DAX

- fully managed in-memory cache for dynamoDB
- only for DynamoDB
- microsseconds latency
- secure, highly scalable and highly available
- DAX is only for and is integrated with DynamoDB

### DynamoDB - Global Tables

- make a DynamoDb table accessible with low latency in multiple regions
- Users can read/write in any table from any region
- 2 way replication
- actively write to any region

## Redshift

- based on PostgreSQL, but it is not used for OLTP - Online Transaction Processing
- OLAP - online analytical processing (analytics and data warehousing)
- Load Data once every hour, not every second
- 10x better performance than other data warehouses scale to PBs of data
- Columnar storage of data (instead of row based)
- Massively parallel query execution (MPP), highly available
- Pay as you go based on instances provisioned
- Has a SQL interface for performing the queries
- BI tools such as AWS Quicksight or Tableau integrate with it

### Redshift Serverless

- Automatically provision and scales data warehouse underlying capacity
- Run analytics workloads without managing data warehouse infrastructure
- pay for only what you use
- use cases: reporting, dashboarding application, real-time analytics

## Amazon EMR

- Elastic MapReduce
- Hadoop Clusters (Big data) to analyze and process vast amount of data
- the clusters can be made of hundreds of EC2 instances
- Also supports Apache Spark, HBase, Presto, Flink...
- EMR takes care of all the provisioning and configuration
- Auto-scaling and integrated with Spot Instances
- use cases: data processing, machine learning, web indexing, big data...

## Amazon Athena

- Serverless query service to perform analytics againts S3 Objects
- uses standard SQL language into query the files
- Supports CSV, Json, ORC, Avro and Parquet
- Load Data in S3 buckets -> Query and analyze with Amazon Athena -> Reporting and dashboards with Quicksight
- 5$ per TB of data scanned
- use compressed or columnar data for cost-savings
- use cases: business intelligence, analytics, reporting, analyze and query VPC Flow Logs...

## QuickSight

- Serverless machine lerning-powered business intelligence service to create interactive dashboards
- create dashboards on your databases
- fast, automatically scalable, embeddable, per-session pricing
- integrated with RDS, Aurora, Athena, Redshift, S3
- BI, visualizations...

## DocumentDB

- MongoDB implementation (similar as Aurora)
- NoSql database
- store, query and index JSON data
- fully managed, highly available with replication across 3 AZs.
- storage automatically grows in increments of 10 GB
- automatically scales to workloads with millions of requests per second

## Amazon Neptune

- fully managed graph database
- graph dataset is similar to a social network
- Available across 3 AZ with up to 15 read replicas
- optimized with complex and hard queries
- can store up to billions of relations and query the graph with millisecond latency
- highly available with replications across multiple AZs
- Great for knowledge graphs (Wikipedia), fraud detection, recommendation engines, social networking

## Amazon Timestream

- Fully managed, fast, scalable serverless time series database
- Automatically scales up/down to adjust capacity
- store and analyze trillions of events per day
- 1000s times faster and 1/10th of the cost of relational databases
- built-in time series analytics functions (identify patterns)

## Amazon QLDB

- Quantum Ledger Database
- a Ledger is a book recording financial transactions
- fully managed serverless, highly available, replication across multiple AZs
- used to review history of all changes made to your application data over time
- Immutable systems, no entry can be removed or modified, cryptographically verifiable
- has a central authority component (central server - source of truth)

## Amazon Managed Blockchain

- multiple parts can execute transactions without the need of trusted, central authority
- descentralized
- join public blockchain networks
- create your own scalable private network
- compatible with: hyperledger Fabric and Ethereum

## AWS GLue

- managed extract, transform and load (ETL) service
- useful to prepare and transform data for analytics
- fully serverless service
- Extract data from S3, RDS, other sources, Glue ETL extract, transform and load it to Redshift (or other service)

## Database Migration Service

- Source DB -> extract data to a Target DB
- Quickly ad securely migrate databases to AWS, resilient, self healing
- the source database remains available during migration
- Supports
  - Homogeneous migration: Oracle to Oracle, Postgres to Postgres
  - Heterogeneous migration: Microsoft to Aurora
