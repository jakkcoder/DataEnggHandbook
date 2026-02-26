# Kafka Offset Management, Distribution, Zookeeper & AWS Basics – Clean Notes

---

## 📌 Offset Management

→ Offset management is used to **track message consumption by each consumer per partition**

→ Offset is a **sequential number** assigned to messages as they arrive in a partition  
→ Once assigned, an offset **cannot be changed**

→ Offset is:
- **Not global**
- **Unique only within a partition**

→ A message is uniquely identified by:
```

Topic Name → Partition Number → Offset

```

---

## 🧠 Broker Tracking of Offsets

→ Kafka broker keeps track of:
- What data is **sent** to a consumer
- What data is **acknowledged** by a consumer

Two important offset states:
- **Current Offset**
- **Committed Offset**

---

### Acknowledgement Handling

→ If Kafka broker does **not receive acknowledgement within a timeout**:
- Broker **resends uncommitted messages**
- Happens in case of:
  - Consumer failure
  - Timeout

---

## ▶️ Consumer Read Options

→ Consumer has the option to read data from:

- **start** → from the beginning
- **latest** → from the most recent offset
- **from-offset** → from a specific offset

---

## 📊 Partition vs Consumer Count

→ Rule:
```

Number of partitions ≥ Number of consumers

```

→ If consumers > partitions:
- Some consumers will remain **idle**

---

## 🔁 Kafka Distribution (Leader–Follower Model)

→ Each partition has:
- **One leader**
- **One or more followers**

---

### Leader Responsibilities

- Handles **all read & write requests**
- Manages partition state

---

### Follower Responsibilities

- **Passively replicate** data from leader
- Do not serve read/write requests

---

### Leader Failure

→ If leader fails:
- One of the followers **automatically becomes the new leader**

---

### Dual Role of Brokers

→ A broker can:
- Act as **leader** for some partitions
- Act as **follower** for other partitions

→ This helps in **load distribution** across the cluster

---

## ⚖️ Load Balancing at Producer End

→ Goal: **spread messages evenly**

Methods:
- **Round-robin approach**
- **Key-based partitioning**
- Explicitly specifying partition number

---

## ⚡ Parallelization

→ Partitioning allows:
- Topic data to be divided into multiple partitions
- Multiple consumers to read data **in parallel**

---

## 🔄 Rebalancing

→ If a consumer:
- Joins the group
- Leaves the group
- Crashes

→ Kafka **rebalances partitions** among consumers  
→ Ensures fair workload distribution

---

## 🐘 Zookeeper

→ Provides:
- Configuration management
- Synchronization service
- Central registry for distributed systems

---

### Role of Zookeeper in Kafka

→ Stores **shared metadata** for:
- Kafka brokers
- Kafka consumers

---

### Broker Management

→ When a broker starts:
- It **registers itself with Zookeeper**

---

### Topic Management

→ All topics and their partitions are:
- **Registered in Zookeeper**

---

## 🧱 Kafka Cluster Types

```

Kafka Cluster Types
/              |               
Single Node     Single Node       Multiple Node
Single Broker   Multiple Broker   Multiple Broker

```

---

## 🔄 Apache Flume

→ Used for **log collection and ingestion**  
→ Commonly used to push logs into:
- HDFS
- Kafka

---

# ☁️ AWS (Amazon Web Services)

---

## 🌐 What is AWS?

→ AWS is a **cloud platform**  
→ Provides a **collection of services**  
→ Multiple services are integrated to form solutions

---

## 🧠 AWS Characteristics

- Cloud-based collection of services
- Solutions built using **different AWS services**
- Services are **independent**
- Services communicate with each other

---

## ⭐ Features of AWS

- **Scalability**
  → Increase compute, VM, and storage resources
- **Cost effectiveness**
- **Time effectiveness**
  → Faster solution implementation using managed services

---

## ☁️ Types of Cloud Deployment

### Private Cloud
→ Owned by organizations  
→ Used for **sensitive data**  
→ Has its own data centers

---

### Public Cloud
→ Owned by cloud providers  
→ Example: **AWS**

---

### Hybrid Cloud
→ Combination of:
- Local (on-prem) infrastructure
- Cloud infrastructure

→ Uses best of both worlds  
→ Often integrated with:
- AWS
- Azure
- GCP

---

## 🚀 Cloud-Native Process

→ Designed to run **natively on cloud**
→ Emphasizes scalability and resilience

---

## 📈 Scalability Models

### Horizontal Scalability
→ Replicating resources with same configuration  
→ Example:
- Adding more VMs  
→ Results in:
- **Zero or minimal downtime**

---

### Vertical Scalability
→ Increasing resource size  
→ Example:
- More CPU
- More memory
- More storage  

→ No replicas or copies created

---

## ✅ Summary

- Offsets uniquely identify messages within partitions
- Brokers track current & committed offsets
- Partitioning enables parallel consumption
- Leader–follower model ensures fault tolerance
- Zookeeper manages Kafka metadata & coordination
- AWS provides scalable, cost-effective cloud services
- Horizontal scaling improves availability; vertical scaling improves capacity
