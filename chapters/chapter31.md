# Performance & Cost Optimization (Spark, Kafka, AWS) – Chapter 31

---

## 🎯 Why Optimization Matters in Data Engineering

→ Data Engineering is not just about correctness  
→ It is about **speed, scalability, and cost control**

Interviewers test:
- Performance bottlenecks
- Trade-offs
- Cost-awareness

---

# ⚡ Apache Spark Optimization

---

## 🧠 Spark Performance Pillars

```

CPU
Memory
Disk
Network (Shuffle)

````

→ Most Spark jobs fail or slow down due to **shuffle & memory issues**

---

## 🔁 Shuffle Optimization (VERY IMPORTANT)

→ Shuffle happens during:
- Joins
- GroupBy
- ReduceByKey
- Window functions

### Reduce Shuffle
- Prefer **broadcast joins**
- Filter data BEFORE joins
- Reduce number of columns early

---

### Shuffle Partitions

Default:
```text
spark.sql.shuffle.partitions = 200
````

→ Too many partitions:

* Small tasks
* Scheduler overhead

→ Too few partitions:

* Large tasks
* OOM errors

👉 Tune based on data size

---

## 📦 Partitioning Strategies

### Repartition

→ Increases or decreases partitions
→ Causes full shuffle

```python
df.repartition(100)
```

---

### Coalesce

→ Reduces partitions
→ No shuffle (faster)

```python
df.coalesce(10)
```

---

## 🧠 Broadcast Join Optimization

→ Small table is sent to all executors
→ Avoids shuffle

```sql
SELECT /*+ BROADCAST(dim) */ *
FROM fact
JOIN dim ON fact.id = dim.id;
```

⚠️ Use only when table fits in memory

---

## 💾 Memory Management

→ Spark memory types:

* Execution memory
* Storage memory

Best practices:

* Cache only reused data
* Unpersist after use
* Avoid caching large unnecessary datasets

---

## 🧠 Persist vs Cache

* `cache()` → Memory only
* `persist()` → Memory + disk options

---

## 🔍 Spark UI (INTERVIEW GOLD)

→ Use Spark UI to analyze:

* Stage execution
* Shuffle read/write
* Skewed partitions
* Task failures

---

## ⚠️ Data Skew

→ One partition holds most data

Symptoms:

* Few tasks run very long
* Others finish quickly

Solutions:

* Salting keys
* Broadcast joins
* Repartition on better key

---

# 🌊 Kafka Optimization

---

## 🧱 Partition Strategy

→ Partitions control:

* Parallelism
* Throughput

Rule:

```
More partitions → More parallelism
```

⚠️ Too many partitions:

* Broker overhead
* Memory pressure

---

## 🔑 Partition Key Choice

→ Bad key → data skew
→ Good key → even distribution

Examples:

* user_id ❌ (hot users)
* hashed(user_id) ✅

---

## ⏱️ Consumer Performance

Tune:

* `max.poll.records`
* `fetch.min.bytes`
* `fetch.max.wait.ms`

Goal:

* Balance latency vs throughput

---

## 🔁 Offset Commit Strategy

* Auto commit → simple, risky
* Manual commit → safer, controlled

👉 Prefer **manual commits** in critical pipelines

---

## ☁️ AWS Cost Optimization

---

## 🪣 Amazon S3 Optimization

### Storage Classes

| Class        | Use Case          |
| ------------ | ----------------- |
| Standard     | Frequent access   |
| IA           | Infrequent access |
| Glacier      | Archive           |
| Deep Archive | Long-term         |

→ Use **Lifecycle policies** to move data automatically

---

## 💻 EC2 Optimization

### Instance Types

* Compute optimized
* Memory optimized
* Storage optimized

👉 Choose based on workload

---

### Spot vs On-Demand

* **On-Demand**
  → Stable, expensive

* **Spot**
  → Cheap, interruptible

Use cases:

* Batch jobs
* Non-critical processing

---

## ⚙️ EMR vs Glue vs Lambda

| Service | Best Use                |
| ------- | ----------------------- |
| EMR     | Long-running big jobs   |
| Glue    | Serverless ETL          |
| Lambda  | Small event-driven jobs |

---

## 📊 Data Warehouse Optimization

---

### Partitioning

→ Partition by:

* Date
* Region
* Customer segment

Benefits:

* Partition pruning
* Faster queries
* Lower cost

---

### Clustering

→ Sort data on frequently filtered columns

Benefits:

* Faster scans
* Reduced IO

---

## 💰 Cost-Aware Querying

→ Avoid:

* SELECT *
* Unfiltered joins
* Cross joins

→ Always:

* Filter early
* Select only required columns

---

## 🧠 Interview Optimization Questions

* How do you optimize Spark joins?
* What causes shuffle?
* How do you handle data skew?
* How do you reduce AWS cost?
* How do partitions affect Kafka throughput?
* When would you use Spot instances?

---

## ✅ Chapter 31 Summary

* Spark bottlenecks = shuffle + memory
* Partitioning strategy is critical
* Broadcast joins improve performance
* Kafka partitions drive parallelism
* Consumer tuning improves throughput
* AWS costs must be actively optimized
* Storage & compute choices matter

