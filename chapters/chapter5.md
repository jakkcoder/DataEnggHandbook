# Hadoop Ecosystem & HDFS – Clean Notes

---

## 🐘 Hadoop Ecosystem

→ Hadoop ecosystem is a collection of tools used for **distributed storage and processing**

---

## 🧮 MapReduce

→ A **programming model** in the Hadoop ecosystem  
→ Used to perform **distributed processing**

Notes:
- Higher-level components → interactivity
- Lower-level components → storage & scheduling

---

## 🧱 Hadoop Components

→ **HDFS**
- Scalable storage
- Stores large number of files
- Handles fault tolerance
- Distributed File System

→ **YARN (Yet Another Resource Negotiator)**
- Resource management & scheduling

→ **Hive**
- Open-source data warehouse
- SQL-like querying

→ **Pig**
- Data cleansing and transformation

→ **Giraph**
- Graphical / graph processing

→ **Storm**
- In-memory / real-time processing tool

→ **Spark**
- Fast in-memory processing engine

→ **MongoDB**
- NoSQL data source

→ **Cassandra**
- Distributed NoSQL database

→ **Zookeeper**
- Mainly used for configuration management

---

## 📂 HDFS (Hadoop Distributed File System)

→ Used for **storage**
→ Files are stored in a **distributed manner**

### Key Characteristics
- Everything in HDFS is a **file**
- Built on **commodity hardware**
- Highly fault tolerant
- Optimized for **batch processing**
- High throughput (not low latency)
- Supports very large datasets

---

## 🗄️ File Storage in HDFS

→ Manages file storage across multiple disks  
→ Disks are spread across machines in a cluster

---

## 🧩 HDFS Nodes

```

```
      HDFS Node
       /     \
 NameNode   DataNode
```

```

### NameNode
- Stores **metadata**
- Maintains file system namespace
- Stores directory structure
- Determines mapping of blocks to DataNodes
- Executes file system operations
- Table of contents of HDFS

### DataNode
- Stores **actual data**
- Physically stores data blocks
- Performs block creation and deletion
- Handles read/write requests
- Reports back to NameNode

---

## 📦 Storing a File in HDFS

→ Distributed files are split into **blocks (data partitions)**

### Block Size
- Default block size: **128 MB**
- Large block size reduces seek time

Effects:
- Increasing block size → reduces parallelism
- Increasing number of blocks → increases parallel processing
- Too many blocks → increases NameNode metadata load

---

## 📖 Reading a File in HDFS

→ Metadata from **NameNode** is used  
→ NameNode provides location of DataNodes  
→ Client directly reads data from DataNodes

---

## ⚠️ Challenges in Distributed Systems

- Failure of NameNode → metadata loss
- Failure of DataNode → data loss

---

## 🛡️ Managing DataNode Failure

→ Use **Replication**

### Replication Factor
- Number of times data is replicated
- Default replication factor in Hadoop: **3**

Replication Strategy:
- Replicas stored on different machines
- Balance between:
  - Redundancy (fault tolerance)
  - Bandwidth usage

---

### Rack Awareness

→ Read requests are routed to the **nearest rack**
→ Improves performance
→ Reduces network bandwidth usage
→ Data is distributed across racks for fault tolerance

---

## 🧠 Managing NameNode Failure

→ Hadoop uses **replication at NameNode level**

### NameNode Files
1. **fsimage**
   - Snapshot of the complete file system at cluster startup

2. **edits**
   - Log of all file system changes during runtime

→ These two together construct the NameNode state

---

## 🔄 Merging fsimage and edits

→ Resource-intensive and time-consuming process

Why merging is required:
- To ensure consistency
- Prevent users from accessing incorrect data

Process:
- Secondary NameNode performs merging
- Merges `fsimage` with `edits`
- This process is called **Checkpointing**

---

### Checkpointing Details

- Happens periodically
- Default interval: **1 hour**
- Interval can be configured

---

## 🔁 Replica Updates

→ When one replica is updated:
- Other replicas are updated asynchronously
- Replicas are stored at different locations

---

## 🔔 Heartbeat Mechanism

→ DataNodes keep sending **heartbeat signals** to NameNode

If heartbeat fails:
- DataNode contacts **Secondary NameNode**
- Secondary NameNode can take over
- Supports high availability

---

## 🚀 Summary

- Hadoop focuses on **high throughput**, not low latency
- Designed for **cheap storage + massive scale**
- Fault tolerance achieved using:
  - Replication
  - Rack awareness
  - Checkpointing
