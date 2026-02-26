# Apache Spark – Joins, Join Strategies & RDD Internals – Clean Notes

---

## 🔗 Spark Joins

→ Same as SQL joins  
→ Difference: **DataFrames are joined instead of tables**

---

## 🔀 Types of Joins in Spark

```

Join Types
|      |        |          |         |          |        |
Inner  Outer   Left Outer  Right Outer Left Semi Left Anti Cross

```

---

### Inner Join
→ Returns **only matching records**
→ Common values in both DataFrames

---

### Outer Join
→ Returns **all records** from both DataFrames  
→ Non-matching values are filled with `null`

---

### Left Outer Join
→ All records from **left DataFrame**  
→ Matching records from right DataFrame

---

### Right Outer Join
→ All records from **right DataFrame**  
→ Matching records from left DataFrame

---

### Left Semi Join
→ Used mainly as a **filter**
→ Returns only columns from **left DataFrame**
→ Keeps rows that have a match in right DataFrame
→ Right DataFrame columns are **not included**

---

### Left Anti Join
→ Returns rows from **left DataFrame that do NOT match**
→ Used for identifying missing records

---

### Cross Join
→ Produces **Cartesian product**
→ Every row from left joined with every row from right
⚠️ Very expensive — use carefully

---

## ⚠️ Challenges in Spark Joins

### Joins on Complex Data Types
→ Complex columns (array / struct) cannot be directly joined  
→ Solution:
- Use `explode()` before join

---

### Duplicate Column Names
Ways to handle:
1. Use **different join expressions**
2. **Drop** duplicate columns after join
3. **Rename** columns before joining

---

## ⚙️ Spark Join Strategies

→ Communication between nodes happens in **two ways**

```

Join Strategies
/                
Shuffle Join     Broadcast Join

````

---

### Shuffle Join
→ Used for **big table ↔ big table**
→ Data shuffled across network
→ Expensive due to data transfer
→ Default strategy if no optimization applies

---

### Broadcast Join
→ Used for **big table ↔ small table**
→ Small table is broadcast to all executors
→ Big table does not shuffle
→ Much faster than shuffle join

---

## 🧠 Spark Join Execution (Logical vs Physical)

→ Spark decides join strategy based on:
- Data size
- Configuration
- Statistics

---

## 🧩 Different Join Algorithms

- **Broadcast Hash Join**
- **Shuffle Hash Join**
- **Shuffle Sort-Merge Join**
- **Broadcast Nested Loop Join**
- **Cartesian Join**

---

## 🧪 Low-Level APIs in Spark

→ Used when Structured APIs (DataFrame/Dataset) are insufficient

### Why Low-Level APIs?

- Need fine control over **data placement**
- Custom transformations
- Maintain legacy codebases
- Advanced debugging

---

## 🧱 RDD (Resilient Distributed Dataset)

→ Immutable, **partitioned collection of records**
→ Operated on in **parallel**
→ Low-level Spark abstraction

---

### RDD Characteristics

- Immutable
- Distributed
- Fault tolerant
- Supports parallel operations

---

### Records in RDD

→ Records are **language objects**
- Java objects
- Scala objects

---

### Limitations of RDD

- No automatic optimization
- No Catalyst optimizer
- No Tungsten execution engine
- More verbose code

---

## 🔁 Spark Context

→ `sc` is the short form of **SparkContext**

Examples:
```scala
sc.parallelize(0 to 9)
sc.parallelize(0 to 9, 10)
````

---

## 🧬 Properties of RDD

### Mandatory Properties

* List of partitions
* Function to compute each split
* List of dependencies on other RDDs

### Optional Properties

* Partitioner (for key-value RDDs)
* Preferred locations for computation

---

## 🧩 Types of RDD

```
RDD
 /         \
Generic   Key-Value
```

→ Key-Value RDD supports more **functional operations**

---

## ❓ When to Use RDD

→ Avoid using RDD unless required
→ Use when:

* Explicit partition control is needed
* Low-level manipulation required

---

## 📥 Creating RDDs

1. Convert DataFrame to RDD (**most preferred**)
2. From local collection
3. From external data source (not recommended)

---

## 🔗 RDD Lineage

→ Graph of all **parent RDDs**
→ Enables **fault tolerance**

Why lineage is useful:

1. Supports in-memory processing
2. Enables recomputation instead of replication
3. Filters can be pushed earlier (optimization)

---

### Failure Recovery

→ If an RDD partition is lost:

* Spark **recreates it from lineage**

---

## 🔄 RDD Transformations

→ Manipulation done using **language-level functions**
→ User must explicitly write logic

### Common Transformations

```
Transformations
 |       |      |        |      |      |
Distinct Filter  Map   FlatMap  Sort  Split
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
* `take()`, `takeOrdered()`, `top()` are commonly used

---

## ✅ Summary

* Spark joins behave like SQL joins on DataFrames
* Broadcast joins are fastest for small tables
* Shuffle joins are expensive
* RDDs provide low-level control but lack optimization
* Prefer DataFrames unless RDDs are strictly required
