# Apache Spark – File Formats, Query Pushdown & Aggregations – Clean Notes

---

## 📦 Columnar File Formats

### Reading & Writing Parquet and ORC

→ **Parquet**
- Optimized for **Spark workloads**
- Best for long-term storage
- Columnar storage improves compression & query speed

→ **ORC**
- Optimized for **Hive workloads**
- Columnar format with efficient indexing

---

## 📄 Unstructured Files

→ Spark allows reading **unstructured files** such as text files  
→ Each line is treated as **one record**

Limitations:
- Only **one column** is allowed
- Cannot directly write multiple structured columns (e.g., integer columns) to text files

---

## 🗄️ Structured Files (Databases)

### JDBC & ODBC

→ **JDBC**
- Java Database Connectivity
- API used for database communication

→ **ODBC**
- Open Database Connectivity
- Introduced by Microsoft

---

### Reading from Databases (JDBC)

Key parameters:
- `format` → `"jdbc"`
- `driver` → e.g., `com.mysql.jdbc.Driver`
- `url`
- `tablename`
- `user`
- `password`

Notes:
- Schema does **not** need to be explicitly provided
- Spark automatically infers schema while reading

---

## 🔽 Query Pushdown

→ Spark analyzes **logical and physical plans**  
→ Pushes filtering logic **down to the data source** whenever possible  

Benefits:
- Reduces data movement
- Filters data **before** creating DataFrames

Example:
- Instead of loading the entire table into Spark
- Spark pushes the query to the database and reads only the required subset

---

### Comparison

→ **RDBMS-level filtering**
- Subset of table created at database level

→ **Spark-level filtering**
- Entire table loaded first, then filtered in Spark

---

## 🔀 Repartition vs Coalesce

### Repartition
→ Used to **increase or decrease** number of partitions  
→ **Shuffle occurs**  
→ Expensive operation

---

### Coalesce
→ Used only to **decrease** number of partitions  
→ No shuffle (or minimal shuffle)  
→ Combines existing partitions

⚠️ Avoid unnecessary shuffling as it is computationally expensive

---

## 📊 Spark Aggregations

To perform aggregation:
1. Specify **key column(s)**
2. Specify **aggregation function**

---

### Aggregation Types

```

Aggregation Types
|     |      |       |        |
Select GroupBy Window GroupingSet Rollup Cube

```

---

### Common Aggregate Functions

- `count()`
- `countDistinct()`
- `approx_count_distinct()` → faster, approximate
- `first()`
- `last()`
- `max()`
- `min()`
- `sum()`
- `sumDistinct()`
- `avg()`

---

## 📈 Statistical Aggregate Functions

### Standard Deviation & Variance
- `var_pop()`
- `var_samp()`
- `stddev_pop()`
- `stddev_samp()`

---

### Skewness & Kurtosis
- `skewness()`
- `kurtosis()`

---

### Covariance & Correlation
- `corr()`
- `covar_samp()`
- `covar_pop()`

---

## 🧮 Grouping

→ Specify column(s) using `groupBy()`  
→ Aggregation applied using `agg()`

Notes:
- Each row belongs to **only one group**

---

## 🪟 Window Functions

→ Used to perform aggregations over a **defined window**

### Difference from GroupBy

| Group By | Window Function |
|-------|----------------|
| Each row belongs to one group | Each row can belong to multiple windows |
| Reduces number of rows | Preserves original row count |

---

### Types of Window Functions

```

Spark Window Functions
/        |        
Aggregate  Analytical  Ranking

```

---

## 🧱 Rollup & Cube

### Rollup
→ Hierarchical / multidimensional aggregation  
→ Example:
- Total across all **dates → countries**

---

### Cube
→ Computes **all possible aggregations**  
→ Produces all permutations & combinations  
→ More expensive than rollup

---

## ✅ Summary

- Parquet & ORC are efficient columnar formats
- Query pushdown minimizes data movement
- Repartition causes shuffle; coalesce avoids it
- Aggregations support statistical & analytical queries
- Window functions preserve row-level detail
- Rollup & Cube enable multidimensional analysis

