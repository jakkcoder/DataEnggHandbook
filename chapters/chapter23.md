# AWS Networking, Databases, Serverless & Big Data Services – Clean Notes

---

## 🌐 Internet Connectivity in AWS

### Internet Gateway
→ Used to **connect a VPC to the internet**

### Route Table
→ Acts as a **mediator** to route traffic to the internet  
→ Controls how traffic flows in and out of subnets

---

### Subnet Types

- **Private Subnet**
  → Does NOT connect directly to the internet

- **Public Subnet**
  → Connected to the internet via Internet Gateway

Notes:
- By default, **all subnets are private**
- NAT always resides in a **public subnet**
- NAT communicates with **private subnets**

---

## 🏷️ Resource Tagging

→ Tags & prefixes help in **better organization** of resources  
→ Commonly used for:
- Cost tracking
- Environment separation (Dev / Test / Prod)

---

## 🌍 IP Version

→ **IPv4 is mainly used** in AWS networking

---

## 📊 Monitoring in AWS

→ Monitoring ensures **operations are observed and optimized**  
→ Used to achieve **TOSOCO**
- Time optimization
- Security optimization
- Cost optimization

→ Every AWS resource has **monitoring mechanisms**

---

## 🧱 Subnet & Route Table Behavior

→ Every time a **custom VPC** is created:
- A **route table is automatically created**

---

### Making a Subnet Public (Custom VPC)

Steps:
1. Launch **Internet Gateway**
2. Attach Internet Gateway to **VPC**
3. Create a **new route table**
4. Add route:
```

0.0.0.0/0 → Internet Gateway

````
5. Associate route table with the **subnet**

→ If later you do NOT want the subnet to be public:
- Simply **remove the route table association**

---

## 🔑 Key Pair Management

To copy key-pair details:
```bash
nano <keypair-name>
````

---

## 🗄️ RDS (Relational Database Service)

→ Used for **relational databases**

### Dataset Considerations

* **Format**
  → Relational / Non-relational DB

* **Size**
  → Amount of data

* **Type of dataset**

  * Real-time data
  * Batch data

---

### RDS Key Points

* AWS offers its own relational DB called **Aurora**
* RDS instances can be launched in **multi-availability zones**
* **Read Replicas**
  → AWS creates replicas of the primary instance
  → Located in different AZs
  → Used only for **read operations**

---

### Features of RDS

* Read replicas
* Security
* Fault tolerance

---

## 🧩 DynamoDB (NoSQL Database)

→ **Non-relational database**

### Keys in DynamoDB

* **Primary Key**
* **Sort Key**

---

### Scan Operation

→ `Scan` is:

* Not time-efficient
* Not cost-efficient

→ Used only when **full table scan** is required

---

## 📣 SNS (Simple Notification Service)

→ Used to build **decoupled systems** in AWS

---

## ⚡ AWS Lambda

→ **Serverless compute service**

Characteristics:

* No need to manage infrastructure
* AWS handles compute & storage
* Trigger-based execution

---

### Lambda Observability

* Triggers are attached to Lambda
* **Log Insights** help determine:

  * Whether Lambda was invoked
  * Whether it ran successfully

---

## 🏞️ Data Lake

→ **Centralized repository**
→ Stores:

* Structured data
* Semi-structured data
* Unstructured data
  → Supports data at **any scale**

---

## 🔄 Data Lifecycle Management (DLM)

→ Manages:

* Big data storage
* Data processing
* Analytics lifecycle

---

### Data Lake Usage Diagram

```
            RDBMS
               ↑
Big Data →  Data Lake  →  ML
Processing      ↓
             Data Warehouse
               ↓
          Log Analytics
```

---

## 🏢 Data Warehouse vs Data Lake

| Data Warehouse  | Data Lake         |
| --------------- | ----------------- |
| More structured | Raw, unstructured |
| Purpose-driven  | Stores everything |
| Schema-on-write | Schema-on-read    |

---

## 🧩 Components of Data Lake

* API & UI
* Entitlements (access control)
* Catalog & search
* Collect & store

---

## 🏬 AWS Big Data Services

### Amazon Redshift

→ Data warehousing service

---

### Amazon EMR

→ Launches clusters for **big data technologies**
→ Used for Hadoop, Spark, etc.

---

### AWS Glue

→ **ETL platform**
→ Used for data preparation and transformation

---

## 🌊 Amazon Kinesis

→ Receives data as **messages**
→ Used for **real-time streaming ingestion**

Data from Kinesis can be sent to:

* S3 buckets
* Databases
* Analytics engines

---

### Kinesis Components / Functionalities

a) **Data Streams**
→ Real-time data streaming

b) **Firehose** (Serverless)
→ Buffers & delivers data directly to destinations

c) **Analytics** (Serverless)
→ Analyze streaming data in real time
→ Supports:

* Automatic scaling
* Low latency

d) **Video Streams**
→ Used for video streaming workloads

---

## 📈 Real-Time Insights

→ Based on:

* Operational data
* Performance metrics

→ Data is:

* Analyzed
* Visualized
* Converted into insights

---

## ✅ Summary

* Internet Gateway + Route Table enable internet access
* Public & private subnets control exposure
* RDS handles relational workloads; DynamoDB handles NoSQL
* Lambda enables serverless execution
* Data Lake stores data of all types at scale
* Redshift, EMR, Glue support analytics & ETL
* Kinesis enables real-time data ingestion and analysis
