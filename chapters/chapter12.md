# Apache Spark Actions & DataFrame Operations – Clean Notes

---

## ▶️ Spark Actions

→ Actions **instruct Spark to compute a result**  
→ To trigger computation, **an action must be executed**

Example:
```python
df.count()   # action
````

Notes:

* Transformations define *what* to do
* **Actions trigger execution**

---

### Types of Actions

```
Actions
 /      |        \
View   Collect   Write
```

→ **Action to View**

* Displays data on the console
* Example: `show()`

→ **Action to Collect**

* Collects data to native objects in the respective language
* Example: collecting Spark output into a Python object

→ **Action to Write**

* Writes output data to external systems
* Examples:

  * SQL tables
  * Files
  * Excel, CSV, Parquet, etc.

---

## 💤 Lazy Evaluation

→ Spark sequences transformations to **minimize computation**
→ Spark does **not** execute transformations immediately
→ Execution happens **only when an action is called**

This behavior is called **lazy evaluation**

Benefit:

* End-to-end **optimization of the entire data flow**

---

## 🔄 DataFrame Transformations – Rows

### Filter Rows

Two equivalent approaches:

```python
df.where("count < 2").show(2)
```

```python
df.filter(col("count") < 2).show(2)
```

---

### Unique Rows

```python
df.select("column_name1", "column_name2").distinct().count()
```

Notes:

* If two columns are selected, `distinct()` returns **unique combinations**

---

### Sorting Rows

→ Default order is **ascending**

Two methods:

```python
df.sort("count").show(5)
```

```python
df.orderBy("count").show(5)
```

Descending order:

```python
from pyspark.sql.functions import desc, asc
df.orderBy(desc("count")).show(5)
```

---

### Random Sampling

→ Used to pick **random records**

Parameters:

* `withReplacement` → `True` / `False`
* `fraction` → proportion of data
* `seed` → for reproducibility

Example:

```python
df.sample(withReplacement=False, fraction=0.1, seed=42)
```

---

### Random Split

```python
df1, df2 = df.randomSplit([0.25, 0.75], seed=42)
```

→ Splits data into multiple DataFrames
→ Fractions should sum approximately to **1**

---

### Multiple Conditions

→ Multiple `where` conditions are treated as **AND** conditions

```python
df.where((col("a") > 1) & (col("b") < 5))
```

---

## 🧾 Different Types of Data

* Boolean
* Numeric
* String
* Date & Timestamp
* Complex
* Null

---

### Boolean Operations

```
Boolean
 /    |    \
AND   OR   TRUE/FALSE
```

---

## 🔢 Numeric Operations

Supported operations:

* Add
* Subtract
* Mean
* Standard Deviation
* Correlation
* Rounding

### Rounding Functions

* `round()`
* `ceil()`
* `floor()`

Examples:

```python
round(2.4)  # 2
round(2.5)  # 3
floor(2.5)  # 2
ceil(2.4)   # 3
```

---

## 📊 describe()

→ Used to calculate **statistical summary**

Returns:

* count
* mean
* standard deviation
* min
* max

Example:

```python
df.describe().show()
```

---

## 🔗 Correlation

→ Measures how one variable **influences another**
→ Variables are DataFrame **columns**

---

## 🔤 String Functions

Common string operations:

* Capitalize words
* Add / remove spaces
* Regular expressions

### Common Functions

* `initcap()` → Capitalizes first letter of each word
* `lower()`
* `upper()`
* `lpad()` → Left pad (based on total length)
* `rpad()` → Right pad
* `trim()`
* `ltrim()`
* `rtrim()`

---

## 🔍 Regular Expressions

→ Used for advanced pattern matching & replacements
→ Works with string columns

---

## 📅 Date & Timestamp

→ Dates & timestamps are stored as **strings** internally
→ Converted during execution

Example:

```python
date_df = spark.range(10) \
  .withColumn("today", current_date()) \
  .withColumn("now", current_timestamp())
```

---

## ✅ Summary

* Actions trigger Spark execution
* Spark uses lazy evaluation for optimization
* DataFrame transformations are immutable
* Sampling, sorting, filtering enable efficient analysis
* Built-in functions simplify numeric, string, and date operations
