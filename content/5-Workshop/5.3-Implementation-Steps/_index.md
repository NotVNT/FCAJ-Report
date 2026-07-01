---
title : "Implementation Steps"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

### Step 1: Set up VPC Private Network and EC2 Servers

Process for building an isolated network environment and core compute servers:

Initialize a VPC with CIDR block **10.0.0.0/16** as the primary private network range.

![VPC List](/images/5-Workshop/5.3-Implementation-Steps/vpc-list.png)
*VPC list showing custom VPC with CIDR 10.0.0.0/16*

Divide subnets into **Public Subnets** (where ALB and NAT Gateway reside for direct Internet access) and **Private Subnets** (where EC2 API and Worker servers are placed for complete isolation from the Internet Gateway).

![Subnets List](/images/5-Workshop/5.3-Implementation-Steps/subnets-list.png)
*List of 6 Subnets distributed between Public and Private tiers*

Configure corresponding Route Tables for Public Subnets pointing to the Internet Gateway, and Private Subnets routing outbound traffic through the NAT Gateway located in the Public Subnet.

Deploy a **t3.micro** EC2 instance in the Private Subnet running **Amazon Linux 2023**. Install Docker and Docker Compose to manage and operate the Spring Boot backend application.

![EC2 Instances List](/images/5-Workshop/5.3-Implementation-Steps/ec2-instances-list.png)
*EC2 Instances list showing moneymanager-app in Running state*

![EC2 Instance Detail](/images/5-Workshop/5.3-Implementation-Steps/ec2-instance-detail.png)
*EC2 instance moneymanager-app detail page showing Private IP address*

The Spring Boot backend is split into two independently running containers: **moneymanager-api** handles HTTP/REST API requests on port 8080 (ALB receives HTTPS traffic from outside and forwards it here), and **moneymanager-worker** consumes messages from the SQS queue and performs periodic background tasks without opening any external ports.

The environment configuration file **/app/.env** is stored directly on the EC2 instance's EBS volume for security, injecting environment variables directly into containers at startup.

### Step 2: Configure RDS MySQL and ElastiCache Redis

Deploy the relational database storage subsystem and high-speed cache:

Initialize an **RDS MySQL 8.0** database, **db.t3.micro** size. This database is placed in a Subnet Group spanning the VPC's Private Subnets to completely prevent external access.

![RDS Databases List](/images/5-Workshop/5.3-Implementation-Steps/rds-databases-list.png)
*RDS Databases list with db-moneymanager MySQL 8.0 instance*

![RDS Instance Detail](/images/5-Workshop/5.3-Implementation-Steps/rds-instance-detail.png)
*RDS instance detail page, Connectivity & security tab*

The RDS MySQL Security Group is configured with full blocking mode, only allowing TCP query requests originating from the EC2 API server's security group on default port **3306**. The API server connection uses **Hibernate JPA** to automatically update database table schemas based on Java Entity classes.

Initialize an **ElastiCache Redis** cluster with **cache.t3.micro** node size running in the Private Subnet partition. The Redis Security Group is configured to only accept internal network connections on port **6379** from the EC2 API.

![ElastiCache Redis List](/images/5-Workshop/5.3-Implementation-Steps/elasticache-redis-list.png)
*ElastiCache Redis OSS caches list with moneymanager-redis cluster*

![ElastiCache Cluster Detail](/images/5-Workshop/5.3-Implementation-Steps/elasticache-cluster-detail.png)
*ElastiCache moneymanager-redis cluster detail page*

Spring Boot API uses Redis as a data caching layer for infrequently changed resources to reduce MySQL IO query load, while also running a Rate Limiting algorithm for Nova Money AI assistant chat conversations to prevent spam attacks that could deplete API keys.

### Step 3: Integrate Amazon DynamoDB and AWS SQS

Set up NoSQL unstructured storage and an event-coordinating message queue system:

On the DynamoDB Console, create two main tables with On-Demand Capacity Mode: **chat_sessions** table storing chat session info (Partition key: id, String type) and **chat_messages** table storing detailed message history (Partition key: id, String type).

![DynamoDB Tables List](/images/5-Workshop/5.3-Implementation-Steps/dynamodb-tables-list.png)
*DynamoDB Tables list showing chat_messages and chat_sessions*

![DynamoDB Chat Messages Detail](/images/5-Workshop/5.3-Implementation-Steps/dynamodb-chat-messages-detail.png)
*chat_messages table detail page*

![DynamoDB Chat Sessions Detail](/images/5-Workshop/5.3-Implementation-Steps/dynamodb-chat-sessions-detail.png)
*chat_sessions table detail page*

Assign DynamoDB read/write permissions to EC2 via IAM Instance Profile. In the Spring Boot backend source code, remove the old MongoDB Atlas connection library, integrate the **AWS SDK v2 for DynamoDB**, and configure a **DynamoDbClient** bean pointing to the Singapore region to store Nova Money virtual assistant conversation history efficiently and cost-effectively.

Create a standard AWS SQS queue named **moneymanager-async-jobs**. To handle messages that fail after multiple retries, configure a Dead Letter Queue (DLQ) named **moneymanager-async-jobs-dlq** linked to the main queue via a Redrive Policy with a maximum of **3 retries**.

![SQS Queues List](/images/5-Workshop/5.3-Implementation-Steps/sqs-queues-list.png)
*SQS Queues list showing moneymanager-async-jobs and corresponding DLQ*

![SQS Main Queue Detail](/images/5-Workshop/5.3-Implementation-Steps/sqs-main-queue-detail.png)
*Main queue moneymanager-async-jobs detail page*

![SQS DLQ Detail](/images/5-Workshop/5.3-Implementation-Steps/sqs-dlq-detail.png)
*Dead Letter Queue moneymanager-async-jobs-dlq detail page*

In the backend application, when a user performs a large financial transaction, the API container serializes the event data into a JSON string and uses the **SqsTemplate** object to push the event into SQS. The Worker container uses the **@SqsListener** annotation to listen to SQS and asynchronously execute tasks such as sending notification emails and recalculating budget jar limits without affecting the user's API response time.

### Step 4: Set up Amazon S3 Security and VPC Endpoints

Establish private network connections optimizing latency and cost for S3 connectivity:

Create an Amazon S3 Bucket named **botdevgroup-documents** in fully private mode (Block Public Access) with **SSE-S3** encryption enabled.

![S3 Buckets List](/images/5-Workshop/5.3-Implementation-Steps/s3-buckets-list.png)
*S3 Buckets list showing botdevgroup-documents and the project's static website bucket*

![S3 Documents Bucket Objects](/images/5-Workshop/5.3-Implementation-Steps/s3-documents-bucket-objects.png)
*Objects stored in the botdevgroup-documents bucket*

![S3 Website Bucket Objects](/images/5-Workshop/5.3-Implementation-Steps/s3-website-bucket-objects.png)
*Objects stored in the botdevgroup.me static website bucket*

Create a **Gateway VPC Endpoint** for S3 and attach it to the Route Table of the Private Subnets in the VPC. The newly added route automatically directs all EC2-to-S3 traffic through AWS's internal network backbone instead of traversing the NAT Gateway to the Internet, cutting 100% of NAT Gateway bandwidth processing costs for S3 traffic and improving file transfer speeds.

Create an **Interface VPC Endpoint** (AWS PrivateLink) in Private Subnets across two different Availability Zones for high availability. This Interface Endpoint allocates private internal IP addresses from the VPC.

![VPC Dashboard List](/images/5-Workshop/5.3-Implementation-Steps/vpc-dashboard-list.png)
*VPC dashboard listing VPCs used for configuring Interface Endpoint PrivateLink*

![VPC Resource Map](/images/5-Workshop/5.3-Implementation-Steps/vpc-resource-map.png)
*Resource map of botdevgroup-vpc showing Subnets, Route Tables, and Endpoint connections*

Configure an **Inbound Resolver** in the Route 53 DNS service to listen for requests from external networks (VPN-connected office), resolving S3's public domain name to the internal IP addresses of the Interface Endpoint ENIs, enabling office workstations to securely upload invoices or download reports over VPN.

Configure **Endpoint Policies** on both VPC Endpoints to only allow upload/read operations targeting the Money Manager project's S3 Bucket, preventing data leakage. Additionally, configure an **S3 Bucket Policy** to absolutely deny all S3 access requests from outside that do not go through the two valid VPC Endpoints.

> See the overall architecture diagram in [5.1 Introduction](../5.1-Introduction/) for a better understanding of how these components connect.
