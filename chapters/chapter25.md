# SQL for Data Engineering – Complete Interview Chapter (Chapter 25)

---

## 🎯 Why SQL Is CRITICAL for Data Engineers

→ SQL is used in:
- Data validation
- Data transformation
- Analytics
- Debugging pipelines
- Interview problem solving

⚠️ Many DE candidates fail interviews due to **weak SQL**, not Spark.

---

## 🔗 SQL JOINs – COMPLETE COVERAGE

```

JOIN TYPES
|       |        |            |             |            |        |
INNER   LEFT    RIGHT        FULL          SEMI         ANTI     CROSS

````

---

## 🔹 INNER JOIN

→ Returns **only matching records** from both tables

```sql
SELECT *
FROM orders o
INNER JOIN customers c
ON o.customer_id = c.id;
````

---

## 🔹 LEFT JOIN

→ All rows from **left table**
→ Matching rows from right table
→ Non-matching rows → `NULL`

```sql
SELECT *
FROM orders o
LEFT JOIN payments p
ON o.id = p.order_id;
```

---

## 🔹 RIGHT JOIN

→ All rows from **right table**
→ Matching rows from left table

```sql
SELECT *
FROM orders o
RIGHT JOIN customers c
ON o.customer_id = c.id;
```

---

## 🔹 FULL OUTER JOIN

→ Returns:

* Matching rows
* Non-matching rows from **both tables**

```sql
SELECT *
FROM a
FULL OUTER JOIN b
ON a.id = b.id;
```

---

## 🔹 CROSS JOIN (Cartesian Product)

→ Every row from left joins with every row from right
⚠️ Very expensive – avoid in production

```sql
SELECT *
FROM a
CROSS JOIN b;
```

---

## 🟡 SEMI JOIN (INTERVIEW FAVORITE)

→ Returns rows from **LEFT table only**
→ Checks **existence**, not values

Equivalent to `EXISTS`

```sql
SELECT *
FROM orders o
WHERE EXISTS (
  SELECT 1
  FROM payments p
  WHERE p.order_id = o.id
);
```

Key points:

* No columns from right table
* Used as **filter**

---

## 🔴 ANTI JOIN (MUST KNOW)

→ Returns rows from **LEFT table that do NOT match**
→ Used to find **missing / unmatched records**

### ✅ Preferred (ANTI JOIN)

```sql
SELECT *
FROM orders o
WHERE NOT EXISTS (
  SELECT 1
  FROM payments p
  WHERE p.order_id = o.id
);
```

---

### ❌ Risky Pattern (Avoid in Interviews)

```sql
SELECT *
FROM orders o
LEFT JOIN payments p
ON o.id = p.order_id
WHERE p.order_id IS NULL;
```

⚠️ Problems:

* Fails with duplicates
* Fails with NULLs
* Poor performance

---

## 🪟 WINDOW FUNCTIONS (NON-NEGOTIABLE)

→ Window functions **do NOT reduce row count**

---

## 🔢 ROW_NUMBER vs RANK vs DENSE_RANK

```sql
ROW_NUMBER() OVER (PARTITION BY user_id ORDER BY ts)
```

| Function   | Behavior      |
| ---------- | ------------- |
| ROW_NUMBER | Always unique |
| RANK       | Gaps allowed  |
| DENSE_RANK | No gaps       |

---

## ⏮️ LAG & LEAD

→ Compare with previous or next row

```sql
LAG(amount) OVER (PARTITION BY user_id ORDER BY date)
LEAD(amount) OVER (PARTITION BY user_id ORDER BY date)
```

Use cases:

* Trend analysis
* Change detection
* Time-series comparison

---

## 📊 GROUP BY – COMMON PITFALLS

### ❌ Incorrect

```sql
SELECT user_id, order_date, COUNT(*)
FROM orders
GROUP BY user_id;
```

→ `order_date` is neither grouped nor aggregated

---

### ✅ Correct

```sql
SELECT user_id, COUNT(*)
FROM orders
GROUP BY user_id;
```

---

## 🔍 WHERE vs HAVING

| WHERE              | HAVING            |
| ------------------ | ----------------- |
| Filters rows       | Filters groups    |
| Before aggregation | After aggregation |

---

## 🏆 TOP-N PER GROUP (CLASSIC QUESTION)

❓ *Latest order per customer*

```sql
SELECT *
FROM (
  SELECT *,
         ROW_NUMBER() OVER (
           PARTITION BY customer_id
           ORDER BY order_date DESC
         ) rn
  FROM orders
) t
WHERE rn = 1;
```

---

## 🔁 DEDUPLICATION PATTERNS

### ❌ Unsafe

```sql
SELECT DISTINCT *
FROM table;
```

---

### ✅ Correct Deduplication

```sql
SELECT *
FROM (
  SELECT *,
         ROW_NUMBER() OVER (
           PARTITION BY key
           ORDER BY updated_at DESC
         ) rn
  FROM table
) t
WHERE rn = 1;
```

---

## ⏱️ RUNNING TOTALS / CUMULATIVE SUM

```sql
SUM(amount) OVER (
  PARTITION BY user_id
  ORDER BY date
  ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
)
```

---

## 🔤 STRING FUNCTIONS (DO NOT MISS)

### Case Manipulation

* `LOWER()`
* `UPPER()`
* `INITCAP()`

---

### Length & Trimming

* `LENGTH()`
* `TRIM()`
* `LTRIM()`
* `RTRIM()`

---

### Substring & Position

* `SUBSTRING(col, start, length)`
* `POSITION(substr IN col)`

---

### Replace & Pattern Matching

* `REPLACE(col, 'a', 'b')`
* `LIKE`
* `ILIKE`
* `REGEXP_REPLACE()`
* `REGEXP_EXTRACT()`

---

### Concatenation

* `CONCAT(a, b)`
* `a || b` (DB-dependent)

---

## 🧪 NULL HANDLING (VERY IMPORTANT)

* `COALESCE(col, 0)`
* `NULLIF(a, b)`
* `CASE WHEN col IS NULL THEN 0 END`

---

## ⚡ SQL PERFORMANCE BASICS (INTERVIEW SAFE)

→ Use `WHERE` early
→ Avoid `SELECT *`
→ Prefer `EXISTS / NOT EXISTS` over joins for filtering
→ Avoid functions on indexed columns
→ Filter before JOIN where possible

---

## 🧠 SQL INTERVIEW MINDSET

Interviewers look for:

* Correct logic
* Edge case handling
* NULL safety
* Performance awareness
* Clear explanation

---

## ✅ Chapter 25 Summary

* SQL is foundational for Data Engineering
* ALL JOIN types must be clear
* **ANTI JOIN & SEMI JOIN are high-signal topics**
* Window functions are mandatory
* String & NULL handling cannot be skipped
* Deduplication & Top-N patterns are asked everywhere

---
