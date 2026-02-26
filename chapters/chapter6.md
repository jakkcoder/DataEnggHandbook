# HDFS Commands, Big Data Development & MapReduce – Clean Notes

---

## 📂 HDFS Commands

→ `hdfs dfs`  
- Used before executing any HDFS command

→ Create directory
```bash
hdfs dfs -mkdir <dir_name>
````

→ Copy file from Linux to HDFS

```bash
hdfs dfs -copyFromLocal <local_path> <hdfs_path>
```

Notes:

* Copying to `/home` in Linux may require permission changes
* First navigate to the Linux directory where the file exists, then copy to HDFS

---

### Directory & File Checks

→ List directories

```bash
hdfs dfs -ls /
```

→ Check if file exists in a directory

```bash
hdfs dfs -ls /<path>
```

---

### Disk & Cluster Information

→ Check HDFS space

```bash
hdfs dfs -df
```

→ Check HDFS health

```bash
hdfs fsck /
```

→ Check Hadoop version

```bash
hadoop version
```

---

### File Operations

→ Create empty file

```bash
hdfs dfs -touchz <file_path>
```

→ View file content

```bash
hdfs dfs -cat <file_path>
```

→ Copy file from HDFS to local (Linux)

```bash
hdfs dfs -copyToLocal <hdfs_path> <local_path>
```

→ Move file from Linux to HDFS (cut + paste)

```bash
hdfs dfs -moveFromLocal <local_path> <hdfs_path>
```

---

## 🏗️ Big Data Development Stages

```
RDBMS
   ↓
Ingestion
   ↓
Storage (HDFS / Cloud)
   ↓
Processing (Hive, Spark, Storm, Pig, MapReduce)
   ↓
Visualization (Tableau, Power BI, Business Objects)
```

Cloud Storage Examples:

* Amazon S3
* Azure Blob
* Google Cloud Storage

---

### Ingestion

→ Process of getting data from various sources into big data storage
→ One common ingestion tool: **Sqoop**
→ Moves data from RDBMS to HDFS

After ingestion:

* Data is distributed into **blocks**

---

### Processing

→ Data is processed based on **business needs**

---

## 🧮 MapReduce

→ Programming model for **distributed processing**

### Two Stages

#### 1️⃣ Map

* Takes input (table, file)
* Produces **key–value pairs**
* Executed in parallel

#### 2️⃣ Reduce

* Takes map output
* Combines values for the same key
* Produces final output

---

### MapReduce Execution Flow

→ Mappers work in parallel
→ Within each mapper, data is processed sequentially
→ Mapper output is **key–value pairs**
→ Results are passed to reducers
→ Reducers group values by key and aggregate

---

## ⚙️ MapReduce Implementation

→ Map logic runs inside **Mapper class**

### Data Types

1. Input key type
2. Input value type
3. Output key type
4. Output value type

→ Reduce logic runs inside **Reducer class**

---

### Cluster Execution

→ Mapper & Reducer run on individual nodes
→ Logic is submitted to the cluster
→ Code is distributed to all nodes

Cluster Management:

* Managed by **YARN**
* YARN allocates hardware resources (CPU, RAM)
* Provides resources to mappers & reducers

---

## 🔢 Number of Mappers & Reducers

→ **Number of Mappers**

* Equal to number of data partitions (blocks)
* Decided by the storage system

→ **Number of Reducers**

* Default: **1**
* Can be configured by user
* Depends on:

  * Data size
  * Performance optimization

---

### Partitioning Logic

→ All mapper output data goes to partitions
→ If reducers increase, partitions increase
→ Example:

* Reducer = 1 → Partition 1
* Reducer = 2 → Partition 1 & Partition 2

---

## 🔄 Shuffle, Sort & Partitioning

→ **Partition**

* Determines which reducer a key goes to
* Uses hash partitioning

→ **Shuffle**

* Moves data from mappers to reducers

→ **Sort**

* Sorts data by key before reducer execution

---

## ➕ MapReduce Combiner

→ Runs **after Mapper and before Reducer**

```
Mapper → Combiner → Reducer
```

### Purpose

* Combines values with the same key locally
* Reduces data transferred to reducer

Notes:

* Combiner logic is similar to reducer
* Improves parallelism
* Reduces network I/O

⚠️ Use combiner carefully:

* Output should not change
* Not suitable for all operations (e.g., average calculation)

---

## ✅ Advantages of Combiner

1. Improves parallelism
2. Reduces data transfer

---

## ⚠️ Important Notes

→ Reducer logic should **not always be used directly as combiner**
→ Output must remain correct
→ For averages, combiner & reducer logic differ
