# ETL vs ELT & Data Pipeline Design Patterns (Chapter 28)

---

## 🎯 Why ETL / ELT Matters in Data Engineering

→ Data Engineers are judged on **how they move, transform, and trust data**

Interviewers look for:
- Correct pipeline choice
- Scalability
- Reliability
- Cost awareness

---

## 🔄 ETL vs ELT (FREQUENTLY ASKED)

```

ETL → Transform BEFORE loading
ELT → Transform AFTER loading

```

---

## 🧱 ETL (Extract – Transform – Load)

### Flow
```

Source → Transform → Target

```

### Characteristics
- Transformations happen **outside the data warehouse**
- Requires compute before load
- Slower for very large datasets

### When ETL is Used
- Legacy systems
- Limited warehouse compute
- Strict transformation logic

Examples:
- Informatica
- Talend
- Custom Spark jobs

---

## 🧱 ELT (Extract – Load – Transform)

### Flow
```

Source → Load → Transform

```

### Characteristics
- Raw data loaded first
- Transformations run **inside warehouse**
- Scales better with cloud warehouses

### When ELT is Used (MODERN STANDARD)
- Cloud-native systems
- BigQuery / Snowflake / Redshift
- Flexible analytics use cases

Examples:
- dbt
- Spark SQL
- Warehouse-native SQL

👉 **ELT is preferred in modern DE interviews**

---

## 🧠 ETL vs ELT Comparison

| ETL | ELT |
|---|---|
Transform before load | Transform after load |
External compute | Warehouse compute |
Rigid | Flexible |
Harder to scale | Cloud-friendly |

---

## 🕒 Batch vs Streaming Pipelines

---

## 📦 Batch Processing

→ Data processed at **intervals**

Examples:
- Daily sales reports
- Nightly ETL jobs

Characteristics:
- High latency
- Easier to debug
- Cost-effective

---

## 🌊 Streaming Processing

→ Data processed **as it arrives**

Examples:
- Fraud detection
- Real-time dashboards

Characteristics:
- Low latency
- Complex state management
- Harder to debug

---

## 🧠 Batch vs Streaming

| Batch | Streaming |
|---|---|
High latency | Low latency |
Simple logic | Complex logic |
Cheap | Expensive |
Easy backfills | Hard backfills |

---

## 🧪 Idempotent Pipelines (VERY IMPORTANT)

→ Running pipeline **multiple times gives same result**

Why needed:
- Retries
- Failures
- Backfills

### Idempotency Techniques
- Use primary keys
- Use merge / upsert
- Delete + insert by partition
- Deduplication logic

---

## 🔁 Backfills & Reprocessing

→ Used when:
- Bug fixes
- Late data
- Logic changes

### Safe Backfill Strategy
1. Isolate affected date range
2. Re-run pipeline only for that range
3. Validate output
4. Promote to production

⚠️ Never blindly backfill entire dataset

---

## ⏳ Late-Arriving Data

→ Data arrives **after expected processing window**

Examples:
- Delayed events
- System outages

### Handling Strategies
- Watermarks (streaming)
- Reprocessing recent partitions
- SCD Type 2 updates

---

## 🧩 Schema Evolution

→ Schema changes over time

Examples:
- New column added
- Column removed
- Data type change

### Safe Practices
- Backward-compatible changes
- Nullable new columns
- Versioned schemas
- Avoid breaking changes

---

## 🧠 Incremental vs Full Load

---

### Full Load
→ Load entire dataset every run

Pros:
- Simple logic

Cons:
- Expensive
- Slow

---

### Incremental Load (PREFERRED)

→ Load only **new or changed data**

Methods:
- Timestamp-based
- ID-based
- CDC-based

---

## 🔁 Change Data Capture (CDC)

→ Capture only changed records from source

Types:
- Inserts
- Updates
- Deletes

Tools:
- Debezium
- Database logs
- Kafka-based CDC

---

## 🧪 Data Validation in Pipelines

→ Validate data at every stage

Checks:
- Row counts
- Null checks
- Duplicate checks
- Range checks

---

## 🧠 Exactly-Once vs At-Least-Once

### At-Least-Once
→ Possible duplicates  
→ Requires deduplication

### Exactly-Once
→ Harder to achieve  
→ Requires:
- Idempotency
- Checkpointing

---

## ⚡ Pipeline Failure Handling

→ Pipelines WILL fail

Best practices:
- Retries with backoff
- Partial reruns
- Alerts & monitoring
- Idempotent logic

---

## 🧠 Interview Design Question Examples

- How would you design a daily ETL pipeline?
- How do you handle late-arriving data?
- How do you backfill safely?
- When do you choose streaming over batch?
- How do you make pipelines idempotent?

---

## ✅ Chapter 28 Summary

- ELT is modern standard
- Batch is simpler; streaming is faster
- Idempotency is critical
- Backfills must be controlled
- Late data must be handled explicitly
- Incremental loads are preferred
- CDC improves efficiency
