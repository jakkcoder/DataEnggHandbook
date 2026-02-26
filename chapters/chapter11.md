
# Apache Spark Core Concepts – Clean Notes

---

## ⚡ Apache Spark Overview

→ Spark is a tool for **parallel data processing** on computer clusters  
→ It is a **unified computing engine**  
→ Not limited to processing only structured data  

→ Spark is widely used for:
- Machine Learning
- Streaming analytics
- ETL batch processing

---

### Memory Handling in Spark

→ Spark tries to hold as much data as possible **in memory**  
→ If data does not fit in memory:
- Intermediate output is written to disk

---

## 📚 Spark Libraries

→ Spark provides multiple built-in libraries:

- **Spark SQL**
- **Spark Streaming**
- **Spark MLlib** → for Machine Learning
- **Spark GraphX** → for graph-based processing
- Can also use **external libraries**

---

## 🧩 Components of Spark

### Low-Level APIs

```

RDD  →  Distributed Variables

```

- RDD (Resilient Distributed Dataset)
- Distributed variables (Broadcast, Accumulators)

---

### Structured APIs

```

DataFrame  →  Dataset  →  SQL

```

- Most commonly used APIs
- Table-like abstraction
- Schema-based

---

### Additional Capabilities

- Streaming
- Advanced analytics
- Rich libraries & ecosystem

---

## 🏗️ Spark Architecture

### Spark Application
→ User-written code to process data

---

### Core Components

- **Driver Process**
- **Cluster Manager**
- **Executors**

---

### Driver Process

→ Acts as the **heart of the Spark application**  
→ Maintains all relevant application metadata  

Responsibilities:
- Runs the `main()` function
- Maintains application state
- Responds to user input
- Analyzes, distributes, and schedules work across executors
- Two-way communication with Cluster Manager

---

### Executors

→ Worker processes that:
- Execute tasks assigned by the Driver
- Perform actual computation
- Report results back to the Driver

---

### Cluster Manager

→ Manages **physical cluster resources**  
→ Allocates CPU, memory, and nodes  

Examples:
- YARN
- Kubernetes
- Standalone Spark

---

## 🌐 Spark Language APIs

→ Language in which Spark code is written  
→ Spark converts it into executable Spark jobs

Supported languages:
- **Scala** (native language of Spark)
- **Python** (supports all Scala constructs)
- **SQL**
- **R** (mainly for analytics)

---

## 🧑‍💻 Spark Session

→ Entry point to execute Spark code  
→ Gateway for all Spark functionalities  

### Types of Spark Session

```

Spark Session
/     
Interactive  Standalone App

````

---

### Interactive Mode

→ Spark session already available  
→ Used via terminal or shell

---

### Standalone Application

→ Spark session explicitly created  
→ Used in IDEs and production jobs

---

## 📊 Spark DataFrames & Partitioning

### DataFrames

→ Part of **Structured APIs**  
→ Table-like data structure  
→ Most widely used Spark abstraction  

Characteristics:
- Data organized into rows & columns
- Schema defines column names & types
- Data is partitioned & distributed across cluster nodes

---

### Partition

→ Collection of rows stored in **one physical chunk**  
→ Spark breaks data into smaller partitions  

Benefits:
- Enables parallelism
- Improves performance

---

## ⚙️ Parallelism in Spark

→ Parallelism depends on:
- Number of partitions
- Number of executors

Examples:
- **1 partition + 100 executors** → Parallelism = 1  
- **Many partitions + 1 executor** → Parallelism = 1  

⚠️ DataFrames do **not** allow manual manipulation of individual partitions

---

## 🔄 Spark Transformations

### Immutable Data Structures

→ Spark data structures are **immutable**  
→ Any change produces a **new DataFrame / RDD**

---

### Transformation

→ Instruction used to modify data  
→ Does **not** execute immediately  
→ Builds execution lineage

Example:
```scala
df.where("number % 2 = 0")
````

→ This is a **filter transformation**

---

## 🔀 Types of Transformations

```
Transformation
   /        \
Narrow      Wide
```

---

### Narrow Transformation

→ Each input partition contributes to **only one output partition**

Example:

* `map`
* `filter`

---

### Wide Transformation

→ Input partition contributes to **multiple output partitions**
→ Causes **shuffle**

Examples:

* `join`
* `groupBy`
* `reduceByKey`

---

## ✅ Summary

* Spark is a fast, in-memory processing engine
* Supports batch, streaming, and ML workloads
* Driver coordinates execution; executors perform work
* DataFrames are immutable and partitioned
* Transformations are lazy and form execution lineage

