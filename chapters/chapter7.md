# Apache Hive – Clean Notes

---

## ⏱️ Latency
→ Latency = **delay time**

---

## 🐝 Hive Overview

→ Open-source **data warehouse** tool  
→ Works on top of **HDFS**  
→ Requires:
- HDFS
- YARN
- MapReduce

→ Hive **stores data in HDFS**  
→ Hive processes data by **converting queries into MapReduce jobs**  
→ HQL (Hive Query Language) is used to interact with Hive  
→ Hive exposes files in HDFS as **tables** to the user  
→ Hive **abstracts MapReduce complexity** from the user

---

## 🆚 Hive vs RDBMS

| Hive | RDBMS |
|-----|------|
| Large datasets | Small datasets |
| Parallel computation | Serial computation |
| High latency | Low latency |
| Read-heavy operations | Heavy read/write |
| Not ACID compliant | ACID compliant |
| Disk-based, cheap storage | Expensive storage |
| Batch processing | Transactional processing |

Notes:
- Hive has high latency because it processes data through MapReduce
- Hive does **not own the data**; data is stored in HDFS
- Limited update operations allowed in Hive
- Subqueries are less used
- Joins are limited
- Fewer constraints compared to RDBMS

---

## 🏗️ Hive Architecture

### 1️⃣ Hive Server
→ Entry point when a query is submitted

### 2️⃣ Driver
→ Receives the query from user  
→ Creates session handle  
→ Sends query to compiler

### 3️⃣ Compiler
→ Parses the query  
→ Performs semantic analysis  
→ Creates execution plan (DAG – Directed Acyclic Graph)

### 4️⃣ Metastore
→ Stores metadata about:
- Tables
- Columns
- Databases
→ Acts as a bridge between:
- Data stored in HDFS
- Tables exposed to users

→ Any database with a **JDBC driver** can be used as a metastore

### 5️⃣ Execution Engine
→ Executes the execution plan  
→ Plan is executed in the form of DAG

---

## 🧑‍💻 Hive Interfaces

→ Hive CLI  
→ Beeline CLI

```bash
beeline -u jdbc:hive2://
````

---

## 🧠 Key Difference

→ Hive works on **distributed data**
→ RDBMS works on **centralized data**

---

## 🧾 Hive Data Types

### Primitive Types

→ **Boolean**

→ **Numeric**

* Tinyint
* Smallint
* Int
* Bigint
* Float
* Double
* Decimal (defines precision)

→ **String Types**

* String → unbounded length (most used in Big Data)
* Char
* Varchar

→ **Timestamp**

* Stored as integer
* Can also be treated as string

→ **Date**

---

## 📦 Data Storage in Hive

→ When tables are created in Hive, data is stored in HDFS under:

```
/user/hive/warehouse
```

### Directory Structure

```
DB_NAME.db
   ↓
TABLE_NAME
   ↓
Data files stored in table
```

→ Everything is stored inside **HDFS**

---

## 📊 Hive Tables

### Managed Table

→ Data is **managed by Hive**
→ Stored in Hive warehouse directory
→ When table is dropped:

* Metadata is deleted
* Data is also deleted

---

### External Table

→ Data is **not managed by Hive**
→ Data stored **outside warehouse directory**
→ External path defined explicitly
→ When table is dropped:

* Only metadata is deleted
* Data remains intact

---

### Temporary Table

→ Exists only for current Hive session
→ Does **not support**:

* Partition
* Index

---

## 📥 Inserting Data into Hive Tables

### Standalone Mode

#### From Files

→ Step 1: Copy file from Linux to HDFS

```bash
hdfs dfs -copyFromLocal <file> <hdfs_path>
```

→ Step 2: Load data from HDFS to Hive table

```sql
LOAD DATA INPATH '<hdfs_path>' INTO TABLE table_name;
```

---

### From Other Tables

→ Insert data directly from one Hive table to another

---

### Managed Table Data Load

→ After loading data:

* File is **moved** into Hive warehouse directory
* Data is deleted from original HDFS location

---

### External Table Data Load

→ Provide HDFS path at table creation
→ Data present in HDFS is automatically mapped
→ No data movement happens

---

## 🆚 Managed vs External Table

| Managed Table               | External Table             |
| --------------------------- | -------------------------- |
| Data inside warehouse       | Data outside warehouse     |
| Hive manages data           | Hive manages only metadata |
| Dropping table deletes data | Dropping table keeps data  |
| Path auto-managed           | Path defined by user       |

Example paths:

**Managed**

```
/user/hive/warehouse/db/table/file.txt
```

**External**

```
/path/in/hdfs/file.txt
```

---

## ✅ Summary

* Hive is best for **batch analytics**
* Built on top of Hadoop ecosystem
* Not suitable for low-latency transactions
* Ideal for large-scale data processing

---
