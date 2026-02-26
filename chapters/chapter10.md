# YARN, NoSQL & Spark – Clean Notes

---

## 🧵 YARN (Yet Another Resource Negotiator)

→ All **physical cluster resources** are managed by a cluster manager  
→ Examples: **YARN**, **Kubernetes**

→ YARN is responsible for:
- Job scheduling
- Resource allocation
- Executing tasks within a Hadoop cluster

---

## 🧩 YARN Components

### Application Master
→ Manages the lifecycle of an application  
→ Negotiates resources with the Resource Manager  
→ Monitors execution and handles task failures

---

### Container
→ Collection of **physical resources**
- RAM
- CPU

→ Resources are invoked by launching a container  
→ Container Launch Context (CLC) is used

---

### Resource Manager
→ Central component of YARN  
→ Responsible for:
- Allocating cluster resources
- Scheduling applications
- Coordinating across the cluster

---

### Node Manager
→ Runs on each node in the cluster  
→ Manages:
- Containers
- Node-level resources  

→ Registers itself with the Resource Manager

---

## 🧠 Resource Manager Internals

```

```
      Resource Manager
       /            \
 Scheduler     Application Manager
```

```

### Scheduler
→ Decides **which job gets resources**
→ Performs scheduling only (no execution)

---

### Application Manager
→ Accepts application submissions  
→ Negotiates the **first container**  
→ Restarts Application Master if a task fails

---

## 🔄 YARN Job Execution Flow

```

Job Submitted
↓
Resource Manager
↓  (finds free node)
Node Manager
↓
Launches Container
↓
Application Master
↓
Executes Tasks

```

→ If more resources are needed:
- Application Master requests additional containers from Resource Manager

---

## ⏱️ Scheduling Policies

### FIFO Scheduler
→ Jobs are processed in **submission order**  
→ Second job starts only after first completes  
→ Rarely used in production

---

### Capacity Scheduler
→ Cluster capacity divided into **queues**  
→ Large job can move between queues  
→ Some queues may remain underutilized

---

### Fair Scheduler
→ Resources shared fairly among jobs  
→ Jobs get equal resource share over time  
→ Suitable for multi-tenant clusters

---

## 🗄️ NoSQL Databases

→ **NoSQL = Not Only SQL**  
→ Less constrained databases

### Why NoSQL?

- Easy & frequent schema changes
- Faster development
- Handles large data volumes
- Schema-less or flexible schema

---

### NoSQL Avoids

- Overhead of ACID transactions
- Complex SQL queries
- Burden of upfront schema design
- Strong DBMS-enforced constraints
- Heavy transactional workloads

---

## 🧱 Types of NoSQL Data Models

### Key-Value Store
→ Simplest model  
→ Hash table-based  
→ Operations: insert, fetch, update  
→ Example: **Amazon DynamoDB**

---

### Column-Family Store
→ Data stored column-wise  
→ Column is the lowest unit of data  
→ Example: **Cassandra**

---

### Graph Database
→ Based on **graph theory**  
→ Highly scalable  
→ No clustering, but vertical scaling  
→ Example: **Neo4j**  
→ Generally **ACID compliant**

---

### Document Store
→ Data stored as documents  
→ Key-value pairs inside documents  
→ Example: **MongoDB**

---

## 📐 CAP Theorem

→ In distributed data storage, **only two of the three** can be achieved at a time:

- **Consistency**
- **Availability**
- **Partition Tolerance**

→ NoSQL systems usually prioritize **2 out of 3**

---

## 🍃 MongoDB

→ Cross-platform  
→ Document-oriented database

Key Concepts:
- **Collection** → Group of documents (like table)
- Collections do **not enforce schema**
- **Document** → Set of key–value pairs
- Documents in the same collection:
  - Can have different fields
  - Can have different structures
- Supports **dynamic schema**

---

## ⚡ Spark

### Why Spark?

→ Addresses shortcomings of MapReduce

#### Limitations of MapReduce
- Everything converted to key–value pairs
- Heavy disk I/O (reads from HDFS)
- Slower due to read/write on disk
- Written only in Java
- No interactivity
- No streaming support

---

## 🚀 Advantages of Spark

→ **Expressive programming**
- 20+ high-level operations
- Fewer lines of code

→ **In-memory processing**
- Intermediate results stored in memory
- Much faster than disk-based processing

→ Efficient memory utilization
→ Faster processing compared to MapReduce

---

### Processing Capabilities

- Batch processing
- Streaming processing
- Final output generation (like MapReduce)

---

### Language Support

→ Not limited to Java  
→ APIs available for:
- Scala
- Java
- Python
- R

---

## ✅ Summary

- YARN manages cluster resources & scheduling
- NoSQL enables flexible, large-scale data storage
- CAP theorem governs distributed systems trade-offs
- Spark provides fast, in-memory, multi-language processing

