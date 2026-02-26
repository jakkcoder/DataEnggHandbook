# Hive Partitioning, Bucketing, Impala & Sqoop – Clean Notes

---

## ❓ Why Partition?

→ Logical organization of data  
→ Improves query performance and optimization  

⚠️ We should **not partition on any random attribute**  
→ Always choose the **most frequently used filter column**

---

## ⚖️ Partitioning Trade-offs

→ **Large number of partitions**
- Increases overhead on the **NameNode**
- Too many directories

→ **Small number of partitions**
- No real query optimization
- No reduction in scanned data

---

## 🔁 Static vs Dynamic Partitioning

### Static Partitioning
- Partition values are known **before loading**
- Data is manually loaded
- Used when partition values are fixed
- Provides **fine-grained control**

---

### Dynamic Partitioning
- Partition values known **only at runtime**
- Hive automatically creates partitions
- Used when loading from existing tables
- Less control over exact partition values
- Partition size depends on incoming data

---

### Enabling Dynamic Partitioning

Two approaches:
1. Set values to `true` via Hive terminal configuration
2. Enable via XML configuration file

---

## 🔍 Show Partitions

```sql
SHOW PARTITIONS table_name;
````

---

## 📥 Insert Data: Static → Dynamic Partition

```sql
INSERT INTO TABLE dynamic_table
PARTITION (state)
SELECT *
FROM static_table;
```

---

## 📊 Static vs Dynamic Partitioning

| Static                         | Dynamic                       |
| ------------------------------ | ----------------------------- |
| Values known beforehand        | Values known at runtime       |
| Manual data load               | Automatic partition creation  |
| Used when partitions are fixed | Used for existing table loads |
| More control                   | Less control                  |

---

## 🧱 Multi-Column Partitioning

→ Data can be partitioned using multiple columns

```sql
CREATE TABLE user_table (
  id STRING,
  cust_id STRING
)
PARTITIONED BY (country STRING, state STRING)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ',';
```

Insert example:

```sql
LOAD DATA LOCAL INPATH '<path>'
INTO TABLE user_table
PARTITION (country='US', state='CA');
```

---

## 🪣 Bucketing

→ Used to split data into **equal-sized chunks**
→ Each bucket is stored as a **file**

Key Points:

* Uses `hash()` function
* Mostly dynamic
* Reduces DataNode overhead
* Increases NameNode overhead

---

### Create Bucketed Table

```sql
CREATE TABLE bucketed_table (
  id INT,
  name STRING
)
CLUSTERED BY (id)
INTO 4 BUCKETS;
```

---

### Load Data into Bucketed Table

```sql
INSERT INTO TABLE bucketed_table
SELECT id, name
FROM non_bucketed_table;
```

---

### Sampling Using Buckets

```sql
SELECT *
FROM bucketed_table
TABLESAMPLE (BUCKET 1 OUT OF 4 ON id);
```

---

## 🔗 Partition + Bucketing Together

```sql
CREATE TABLE combined_table (
  id INT,
  name STRING,
  cost DOUBLE
)
PARTITIONED BY (category STRING)
CLUSTERED BY (id)
INTO 4 BUCKETS;
```

---

## 🆚 Partition vs Bucket

| Partition            | Bucket                    |
| -------------------- | ------------------------- |
| Logical grouping     | Physical grouping         |
| Creates directories  | Creates files             |
| Best for filtering   | Best for joins & sampling |
| Reduces scanned data | Improves join performance |

---

## ⚡ Impala

→ Parallel SQL processing engine
→ Directly reads data from **HDFS**
→ Uses **Hive Metastore**
→ Hive tables are accessible from Impala

Characteristics:

* Very **low latency**
* Suitable for **small/medium datasets**
* Not ideal for batch-heavy workloads

Comparison:

* Hive → Reliable for batch processing
* Impala → Fast interactive analytics

---

## 🔄 Sqoop

→ Data ingestion tool
→ Transfers data between **RDBMS and Big Data ecosystem**

### Features

* Bulk import & export
* Supports Data Warehouse & NoSQL systems
* Connector-based architecture (plugin support)

---

### Sqoop Working

→ Data split into partitions
→ Map-only job is launched
→ Each mapper handles one partition

---

### Data Type Handling

→ Data types remain consistent during transfer
→ Uses JDBC connector
→ Data transferred in a **type-safe** manner

---

### Performance Consideration

→ Number of splits = Number of mappers
→ Mapper count decided by developer based on data size

---

## ✅ Summary

* Partitioning enables query pruning
* Bucketing improves joins & sampling
* Impala offers low-latency analytics
* Sqoop enables efficient RDBMS ↔ Big Data transfer

---
