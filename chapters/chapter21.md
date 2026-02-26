# AWS Core Concepts, S3 & EC2 – Clean Notes

---

## ☁️ AWS Core Services

AWS broadly provides:

- **Compute**
- **Storage**
- **Networking**
- **Database**
- **Basic Services**

---

## 📈 Elasticity

→ When the **number of users increases**, the application automatically **scales up**  
→ When usage decreases, resources are **scaled down**  

→ This automatic scaling up & down of resources is called **Elasticity**

---

## 📏 Scalability

→ Scalability can be:
- **Automatic**
- **Manually configured**

→ Ensures the system can handle **increasing workload**

---

## 🔐 Core Cloud Principles

- **Availability**
- **Durability**
- **Security**
- **Mobility**

---

## 🌍 Regions & Availability Zones

### Region
→ A geographical area  
→ Each region contains **multiple availability zones**

---

### Availability Zone (AZ)
→ Each AZ contains:
- One or more **data centers**

---

### Region Selection

→ Region choice is **very important**  
→ Depends on:
- Client location
- Latency requirements
- Compliance

→ Region should be **nearest to the user**

---

### Disaster Recovery

→ AWS supports **replication & backup**
→ In case of disaster:
- Data can be **lifted and shifted** to another region

---

## 🔒 Data Protection

- **Data at Rest**
- **Data in Flight**

---

## 🪣 Amazon S3 (Simple Storage Service)

→ Belongs to **Storage services**  
→ Object-based storage service  

Key points:
- Stores data in **any format**
- Highly **scalable**
- **Highly durable**
- Bucket is the **container**
- Object is the **child**

→ S3 is a **service**, not a platform

---

### S3 Use Cases

- General-purpose storage
- Backup & archival
- Static website hosting

---

### S3 Characteristics

→ **Object Storage**
→ Entire object is stored as a single unit  
→ Best storage service in AWS for unstructured data

---

### Bucket Details

→ A bucket can contain up to **5 TB per object**

---

## 🧠 TOSOCO Principle

```

T O S O C O
| | | | |
Time
Optimization
Security
Optimization
Cost
Optimization

```

---

## 🌎 AWS Region Example

→ **US-East (N. Virginia)** → `us-east-1`  
→ Best region for:
- Testing
- Learning
- Cost optimization

---

## 🧱 Object Lifecycle Management (OLM)

→ Used to **manage lifecycle of S3 objects**
→ Automatically moves objects between:
- Storage classes
- Archival tiers

---

## 💻 Amazon EC2 (Elastic Compute Cloud)

→ EC2 belongs to **Compute services**

---

### EC2 Basics

→ EC2 provides **virtual machines (instances)**  
→ Instance configuration can be chosen:
- CPU
- Memory
- Storage

---

### OS & Configuration

→ **OS cannot be changed** after instance creation  
→ **Instance size can be changed**

---

### Changing Region

→ To move EC2 to another region:
- Create an **AMI (Amazon Machine Image)**
- Launch instance in the new region using AMI

→ AWS provides **30+ default AMIs**

---

## 🔑 Key Pair

→ Security credentials for EC2 instance  
→ Can use an **existing key pair**

---

## 🔐 Connecting to EC2

### Linux VM
- SSH connection
- EC2 Instance Connect (browser-based)

### Windows VM
- Remote Desktop Client
- Username & password

---

## 📦 EBS (Elastic Block Store)

→ Persistent storage for EC2  
→ Stores:
- VM data
- Metadata

→ EBS volumes:
- Can be **detached**
- Can be **reattached**
- Can be **resized**

---

### EBS & AMI

→ EBS is used to create **AMI images**
→ AMIs can be:
- Stored in S3 for archival
- Shared or moved to another region

---

## 🚀 Launching EC2 Instances

Ways to launch EC2:

- **Quick Start**
- **My Community AMIs**
- **Marketplace** (500+ tools & technologies)
- **Custom AMI**

---

## ⭐ Features of EC2

- Has its own storage (EBS)
- Supports image creation
- Supports OS & configuration customization
- Extra storage can be attached
- Volumes can be resized

---

## 🧠 Object Storage vs Block Storage

| Object Storage (S3) | Block Storage (EBS) |
|--------------------|-------------------|
| Entire object stored | Data stored in blocks |
| S3 uses this | EC2 uses this |
| Best for unstructured data | Best for OS & VM data |

---

## 🔗 Summary

- AWS provides scalable cloud services
- Elasticity allows automatic scale up/down
- Regions & AZs ensure availability
- S3 is object-based, highly durable storage
- EC2 provides flexible virtual machines
- EBS provides block-level persistent storage
- AMIs help in backup, cloning, and migration
