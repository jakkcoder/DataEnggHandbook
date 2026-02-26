# Oozie & Spark Streaming – Clean Notes

---

## 🧭 Oozie (Scheduler)

→ Part of the **Hadoop Ecosystem**  
→ Used to **schedule, execute, and manage Hadoop jobs** in a distributed environment  

Supported job types:
- MapReduce jobs
- Hive jobs
- Pig jobs
- Shell jobs

---

### Responsibilities of Oozie

→ Allows combining multiple complex jobs into a **sequential workflow**  
→ Responsible for **triggering workflow actions**  
→ Uses Hadoop execution engine to **actually execute tasks**

---

## 📂 Types of Oozie Jobs

1. **Oozie Workflow Jobs**
2. **Oozie Coordinator Jobs**
3. **Oozie Bundle**

---

## 🔁 Oozie Workflow Jobs

→ Workflow is a **sequence of actions**  
→ Represented as a **DAG (Directed Acyclic Graph)**  
→ Specifies the **order of execution**

### Workflow Structure

→ Workflow **always starts with `<start>` tag**  
→ Workflow **always ends with `<end>` tag**

```

Workflow
/        
Controls    Actions

```

---

### Control Nodes (control the workflow)

- `start`
- `decision`
- `fork` → multiple paths in parallel
- `join`
- `end`
- `kill`

---

### Action Nodes (actual execution)

- Hive job
- Shell job
- Pig job

---

### Workflow Characteristics

→ Workflow can be **parameterized**  
→ Hardcoding values is **not necessary**

---

## ⏱️ Synchronous vs Asynchronous

→ **Synchronous**
- Tasks executed one after another
- Caller waits for completion

→ **Asynchronous**
- Tasks executed independently
- Caller does not wait

---

## 🔀 Workflow Execution Types

→ Oozie workflow supports **two execution types**:
- Synchronous
- Asynchronous

---

## 📌 States of a Workflow

- Succeeded
- Suspended (environmental issues)
- Killed (manual termination)
- Failed
- Running

---

## ⏰ Oozie Coordinator Jobs

→ Workflow triggered by **time and/or data availability**  
→ Example:
- Run job every hour
- Trigger when data arrives

---

## 📦 Oozie Bundle

→ Logical grouping of:
- One or more workflows
- One or more coordinators

→ Used to manage **related jobs together**

---

# 🌊 Spark Streaming

---

## 🔄 What is Stream Processing?

→ Processing data **as it is being generated**  
→ Input data is **unbounded**
→ No predefined beginning or end  

Example:
- Credit card transactions

---

### Continuous Applications

→ Can perform:
- Batch processing
- Stream processing
- Interactive processing

---

## 📌 Use Cases of Spark Streaming

- Notification & alerting
- Real-time reporting
- Incremental ETL
- Real-time decision making (e.g., Google Maps)
- Online Machine Learning

---

## ✅ Advantages of Stream Processing

→ **Lower latency** compared to batch processing

---

## ⚠️ Challenges of Stream Processing

- Maintaining large amounts of state
- Supporting high data throughput
- Handling **out-of-order data**
- Responding with low latency
- Joining streaming data with external storage
- Updating business logic dynamically

---

# 🧱 Structured Streaming

---

## 📘 What is Structured Streaming?

→ Structured Streaming provides:
- **End-to-end exactly-once semantics**
- **Fault tolerance** via checkpointing

→ Treats streaming data as a **continuously growing table**

---

### Key Properties

→ Most transformations are **similar to batch processing**  
→ Spark handles **incremental processing internally**

---

## 🧠 Core Concepts of Structured Streaming

### Transformations & Actions
→ Same transformations as batch  
→ **Only one action** is supported: writing the stream

---

### Input Sources

Supported sources include:
- Apache Kafka
- Files (HDFS, S3, etc.)
- Distributed file systems
- Socket source (for testing)

---

### Sink

→ Destination where output is written  
→ Examples:
- Kafka
- File system
- Console sink

---

### Execution Engine

→ Responsible for:
- Tracking progress
- Managing state
- Ensuring fault tolerance

---

### Output Modes

→ Defines **how data is written to the sink**

---

### Triggers

→ Define **when data is written**
→ Example:
- Every X seconds
- Once
- Continuous

---

### Event-Time Processing

→ Supports **event-time semantics**  
→ Data processed based on **timestamp in record**  
→ Handles **late-arriving and out-of-order data**

---

## 🔌 Supported Sinks

- Apache Kafka
- Any file format
- Console sink

---

## ✅ Summary

- Oozie is used for workflow scheduling in Hadoop
- Workflows are DAG-based with control and action nodes
- Coordinators trigger workflows based on time/data
- Spark Streaming processes unbounded data in real time
- Structured Streaming offers exactly-once semantics
- Event-time processing handles late and out-of-order events
