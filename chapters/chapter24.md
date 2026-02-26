# Amazon Kinesis, EC2 vs EBS & AWS Data Migration – Clean Notes

---

## 🌊 Amazon Kinesis – Overview

### Consumers of Kinesis Data
→ Consumers can be:
- S3
- Redshift
- EBS
- DynamoDB

→ **Working entity for Kinesis Firehose**
- Delivers data in **clean / transformed** form

---

## 📥 Kinesis Data Streams

→ Used to **collect streaming data** and dump it to targets  
→ Mainly used for **data ingestion**

Examples:
- Bank transactions
- Application logs

Key points:
- Managed service
- Requires configuration
- Used when **real-time ingestion** is needed

---

## 🚚 Kinesis Firehose

→ **Data transfer service**  
→ Used to load streaming data into:
- Amazon S3
- Amazon Redshift
- Other supported destinations

Characteristics:
- **Unlimited scalability**
- Fully managed service
- **No admin or cluster management required**

---

## 🎥 Kinesis Video Streams

→ Provides a **use-case-specific platform**
→ Ability to stream **video data**
→ Example:
- Streaming video from cameras
- Integrated with Amazon services

---

## ⚙️ Kinesis Data Streams (Detailed)

→ Used to collect data streams from:
- Servers
- Mobile devices
- IoT devices

→ Provides a platform for **continuous data processing**

→ Elastic service:
- Resources automatically increase as data increases

---

## 🧩 Kinesis Internals

### Shard
→ **Working entity of Kinesis Data Streams**

### Partition Key
→ Used to decide **which shard** will receive the data

### Sequence Number
→ Ensures **ordering of records within a shard**

---

## 💻 EC2 vs EBS (Quick Comparison)

### EC2
- When VMs are launched, they are **blank**
- OS & software must be **installed and configured**
- Partially managed

---

### EBS (Elastic Block Store)
- Has its **own infrastructure**
- No OS installation required
- **Highly managed** storage service

---

## 🪣 Amazon S3 (Note)

→ S3 **always works online**  
→ Designed for **high availability**

---

## 🧮 Sharding Logic

→ Sharding decides **which data will be picked**
→ Based on:
- Partition key
- Hashing logic

---

## 🔗 VPC Endpoint

→ Enables services inside a VPC to:
- Communicate with each other **privately**
- Without using the public internet

Benefits:
- No need to set up **NAT Gateway**
- Improved security
- Reduced latency

---

## 🛡️ AWS Shield

→ **Backend security service**
→ Protects AWS resources from:
- **DDoS attacks**

---

## ☁️ Cloud Data Migration

### Backup / Data Transfer Services

---

### AWS Storage Gateway
→ Used when **files / snapshots** need to be migrated  
→ Acts as a bridge between on-premises and AWS

---

### AWS Direct Connect
→ Used when **datacenter-level migration** is required  
→ Provides a **dedicated network connection** to AWS

---

### Amazon S3 Transfer Acceleration
→ Accelerates **long-distance data transfers** to S3  
→ Uses AWS global edge locations

---

### AWS Transfer Family
→ Secure transfer service
→ Supports:
- SFTP
- FTPS
- FTP

---

### AWS DataSync
→ Automates data movement between:
- On-premises storage
- AWS storage services

---

## 🚚 Offline Migration Services

### AWS Snowcone
→ Small, portable data transfer device

### AWS Snowball
→ Medium-scale data transfer device

### AWS Snowmobile
→ Exabyte-scale data migration
→ Physical data center on a truck

---

## ✅ Summary

- Kinesis supports real-time data ingestion and streaming
- Shards are the fundamental unit of Kinesis Data Streams
- Firehose is fully managed and delivery-focused
- EC2 provides compute; EBS provides block storage
- VPC Endpoints enable private AWS service access
- AWS Shield protects against DDoS attacks
- AWS provides both online and offline data migration services
