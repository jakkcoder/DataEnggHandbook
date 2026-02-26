# Apache Spark – Joins, Join Strategies & RDD Internals (Clean Notes)

---

## 🔗 Spark Join

→ Same as SQL joins  
→ Difference: **instead of tables, DataFrames are joined**

---

## 🔀 Join Types

```

Join Types
|      |        |           |            |           |        |
Inner  Outer   Left Outer   Right Outer   Left Semi   Left Anti  Cross

```

### Inner Join
→ Returns **only matching records**

### Outer Join
→ Returns **all records from both sides**
→ Non-matching values are filled with `null`

### Left Outer Join
→ All records from **left DataFrame**
→ Matching records from right DataFrame

### Right Outer Join
→ All records from **right DataFrame**
→ Matching records from left DataFrame

### Left Semi Join
→ Used **more like a filter**
→ Only matching rows from **left table**
→ Only **left table columns** appear in result

### Left Anti Join
→ Returns **non-matching records**
→ Only records from **left table** that do NOT match

### Cross Join
→ Cartesian product
→ Every row from left joins with every row from right
⚠️ Very expensive

---

## ⚠️ Challenges in Joins

### Joins on Complex Types
→ Complex columns (array / struct) cannot be joined directly  
→ Solution:
```

explode() → then join

```

---

### Handling Duplicate Columns

Options:
1. Use **different join expressions**
2. **Drop** duplicate columns after join
3. **Rename** columns before join

---

## ⚙️ Spark Join Strategies

→ Communication in Spark happens in **two ways**

```

Join Strategies
/            
Shuffle Join   Broadcast Join

````

---

### Shuffle Join
→ **Big table ↔ Big table**
→ Data shuffled across the network
→ Expensive because **data transfer occurs**

---

### Broadcast Join
→ **Big table ↔ Small table**
→ Small table is **broadcast to all executors**
→ Big table does not shuffle
→ Much faster than shuffle join

---

## 🧠 Different Join Algorithms

→ Spark can choose among:

- Broadcast Hash Join
- Shuffle Hash Join
- Shuffle Sort-Merge Join
- Broadcast Nested Loop Join
- Cartesian Join

→ Selection depends on:
- Data size
- Statistics
- Spark configuration

---

## 🧪 Low-Level APIs

### RDD – Manipulating Distributed Data

→ Used when functionality **cannot be done using Structured APIs**  
→ Provides control over **physical data placement** across cluster  

Why low-level APIs?
- Maintain **legacy codebases**
- Custom data manipulation
- Easier debugging in some scenarios

⚠️ Spark internally converts DataFrames to RDDs,  
but **users should not rely on RDDs unless required**

---

## 🧱 RDD (Resilient Distributed Dataset)

→ Immutable, partitioned collection of records  
→ Can be processed in parallel  

Characteristics:
- Immutable
- Distributed
- Fault tolerant

Notes:
- In RDD, records are **language objects** (Java / Scala)
- No automatic optimization (unlike DataFrames)
- No Catalyst optimizer

---

## 🔑 Spark Context

→ `sc` = **SparkContext**

Examples:
```scala
sc.parallelize(0 to 9)
sc.parallelize(0 to 9, 10)
````

---

## 🧬 Properties of RDD

### Mandatory

* List of partitions
* Function to compute each split
* List of dependencies on other RDDs

### Optional

* Partitioner (for key-value RDD)
* Preferred locations for computation

---

## 🧩 Types of RDD

```
RDD
 /        \
Generic   Key-Value
```

→ Key-Value RDD has **more functional operations**

---

## ❓ When to Use RDD

→ **Do not use RDD unless required**

Use RDD when:

* Explicit partition control is needed
* Low-level transformations are required

---

## 📥 Creating RDDs

Preferred order:

1. **Convert DataFrame to RDD** (most preferable)
2. RDD from local collection
3. RDD from data source (not advisable)

---

## 🔗 RDD Lineage

→ Graph of all **parent RDDs** of an RDD
→ Enables **fault tolerance**

Why lineage?

1. Supports in-memory processing
2. If a partition is lost, Spark **recreates it**
3. Enables optimization (e.g., filter pushdown)

---

## 🔄 RDD Transformations

→ Manipulation done using **language-level functions**
→ User explicitly writes logic

### Types of Transformations

```
Transformations
 |        |      |         |      |      |
Distinct Filter  Map    FlatMap  Sort   Split
```

Examples:

* `distinct()`
* `filter(word => word.startsWith("a"))`
* `map(word => (word, 1))`
* `flatMap()`

---

## ▶️ RDD Actions

```
Actions
 |        |      |        |        |
Reduce  Count  First  Max/Min   Take
```

Notes:

* `reduce()` is **not deterministic**
* Common actions:

  * `take()`
  * `takeOrdered()`
  * `top()`

---

## ✅ Summary

* Spark joins mirror SQL joins on DataFrames
* Broadcast join is fastest for small tables
* Shuffle join is expensive due to data transfer
* RDDs provide low-level control but lack optimization
* Prefer DataFrames unless RDDs are absolutely required

---
