# Hive Data Loading, Complex Data Types & Query Optimization – Clean Notes

---

## 🔁 Data Insertion: Table to Table

```sql
CREATE TABLE new_table (
  id STRING,
  title STRING
);

INSERT INTO TABLE new_table
SELECT id, title
FROM source_table;
````

---

## 📥 Loading Data into Hive Tables

### From Files (Linux → HDFS → Hive)

→ Step 1: Copy file from Linux to HDFS

```bash
hdfs dfs -copyFromLocal <file_path> <hdfs_path>
```

→ Step 2: Load data from HDFS into Hive table

```sql
LOAD DATA INPATH '<hdfs_path>' INTO TABLE table_name;
```

---

### Load Data Directly from Linux (Local)

```sql
LOAD DATA LOCAL INPATH '<local_file_path>'
INTO TABLE table_name;
```

---

## 🧩 Complex Data Types in Hive

### Supported Complex Types

→ **Array**

* Collection of elements of the **same type**
* Mostly primitive types allowed

→ **Map**

* Unordered collection
* Stored as **key–value pairs**

→ **Struct**

* Grouping of multiple fields
* Can have **different data types**
* Similar to a list or record

→ **Union**

* Can store one of many data types (not commonly used)

---

### Syntax Example

```sql
CREATE TABLE sample_table (
  id STRING,
  name STRING,
  colors ARRAY<STRING>,
  features MAP<STRING, BOOLEAN>,
  address STRUCT<street:STRING, city:STRING>
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
COLLECTION ITEMS TERMINATED BY '#'
MAP KEYS TERMINATED BY ':';
```

→ After table creation, data can be loaded into the table.

---

## 🧮 Hive Built-In Functions

### UDF (User Defined Functions)

→ Works on **single row**
→ Produces **single output**

Examples:

* `trim()`
* `concat()`
* `length()`
* `round()`
* `floor()`

---

### UDAF (User Defined Aggregate Functions)

→ Works on **multiple rows**
→ Produces **single output**

Examples:

* `avg()`
* `count()`

---

### UDTF (User Defined Table-Generating Functions)

→ Works on **single row**
→ Produces **multiple rows**

Examples:

* `explode()`
* `posexplode()`

---

## 🔎 explode() Function

→ Flattens arrays and maps
→ Creates a **virtual table**
→ Used with `LATERAL VIEW`

Example:

```sql
SELECT id, variant
FROM table_name
LATERAL VIEW explode(colors) color_table AS variant;
```

→ Works with **array & map**

---

## 🔢 posexplode() Function

→ Similar to `explode()`
→ Also returns **index (position)**

Example:

```sql
SELECT pos, variant
FROM table_name
LATERAL VIEW posexplode(colors) color_table AS pos, variant;
```

→ Works only with **arrays**

---

## 🗃️ Denormalization in Hive

→ Data is compressed into **fewer tables**
→ Read in a **single operation**
→ Disk space is cheap in Big Data
→ No foreign key constraints
→ Used to improve performance

Reason:

* As data size increases, disk seek time increases
* Normalization increases joins → slower queries
* Hence Hive prefers **denormalized & complex data structures**

---

## ⚙️ Query Optimization in Hive

### Need for Optimization

* MapReduce jobs take a lot of time
* Debugging is difficult

---

### Ways to Optimize Queries

→ **Design tables properly**

* Partitioning
* Bucketing

→ **Structure queries efficiently**

* Join optimization
* Window functions

---

## 🔗 Join Operations in Hive

→ Joins are expensive due to **shuffle overhead**

Strategy:

* Store smaller tables in memory
* Structure queries to reduce data movement
* Prefer **map-side joins** when possible

---

## 📂 Partitioning & Bucketing

### Partitioning

→ Logical grouping of data
→ Similar to indexes in RDBMS
→ Created during table creation

Example:

```sql
PARTITIONED BY (state CHAR(2))
```

→ Each partition creates a **separate directory**

---

### Standalone Partition Example

```sql
CREATE TABLE user_table (
  id STRING,
  name STRING
)
PARTITIONED BY (state CHAR(2));
```

Insert example:

```sql
INSERT INTO TABLE user_table
PARTITION (state='CA')
VALUES ('1', 'Jay');
```

---

### Partitioning from Files

```sql
CREATE TABLE user_table (
  id STRING,
  name STRING
)
PARTITIONED BY (state CHAR(2))
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ',';
```

---

## 🆚 Partition vs Index

| Partition                   | Index                            |
| --------------------------- | -------------------------------- |
| Affects physical storage    | Does not affect physical storage |
| New directory per partition | Uses additional data structure   |
| No extra lookup structure   | Stores indexed column copy       |
| Best for huge datasets      | Suitable for smaller datasets    |

---

## ✅ Summary

* Hive supports complex data types for efficient storage
* explode / posexplode simplify nested data
* Denormalization improves performance
* Partitioning & bucketing are key for optimization
* Proper query design reduces MapReduce overhead

---
