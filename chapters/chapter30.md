# Data Quality, Reliability & Monitoring (Chapter 30)

---

## 🎯 Why Data Quality Matters in Data Engineering

→ Data pipelines are successful **only if data is trusted**

Bad data causes:
- Wrong business decisions
- Loss of credibility
- Reprocessing & downtime

⚠️ Interviewers expect Data Engineers to **own data quality**

---

## 🧠 Data Quality vs Data Reliability

| Data Quality | Data Reliability |
|---|---|
Correctness of data | Consistency & availability |
Accuracy | Timely delivery |
Completeness | Fault tolerance |

---

## 🧪 Core Data Quality Dimensions

---

### ✅ Completeness
→ Are all required records present?

Example:
- Missing orders
- Missing customer IDs

---

### ✅ Accuracy
→ Does data reflect real-world values?

Example:
- Incorrect prices
- Wrong timestamps

---

### ✅ Consistency
→ Same data should match across systems

Example:
- Revenue mismatch between tables

---

### ✅ Timeliness
→ Is data arriving **on time**?

Example:
- Daily report delayed

---

### ✅ Uniqueness
→ No duplicate records

Example:
- Same order_id appearing multiple times

---

## 🔍 Common Data Quality Checks (INTERVIEW MUST)

---

### Null Checks
→ Critical columns should not be NULL

```sql
WHERE customer_id IS NULL
````

---

### Duplicate Checks

→ Identify duplicate primary keys

```sql
COUNT(*) > 1
```

---

### Range Checks

→ Values within expected range

Example:

* Price > 0
* Age between 0–120

---

### Referential Integrity

→ Foreign keys must exist in dimension tables

Example:

* fact_orders.customer_id exists in dim_customer

---

### Schema Validation

→ Ensure schema has not changed unexpectedly

Examples:

* Missing columns
* Wrong data types

---

## 📏 Data Freshness

→ Measures **how recent data is**

Example:

* Last updated timestamp

```sql
MAX(updated_at)
```

⚠️ Stale data is often worse than no data

---

## ⏱️ SLAs, SLOs & SLIs (INTERVIEW FAVORITE)

---

### SLA (Service Level Agreement)

→ Business-level promise

Example:

* Data available by 9 AM

---

### SLO (Service Level Objective)

→ Target metric

Example:

* 99% daily jobs finish on time

---

### SLI (Service Level Indicator)

→ Actual measurement

Example:

* Job completion time

---

## 🔄 Handling Pipeline Failures

→ Failures WILL happen

Reasons:

* Network issues
* Bad source data
* Resource exhaustion

---

### Failure Handling Strategies

* Retries with backoff
* Partial reruns
* Partition-level reruns
* Alerts & notifications

---

## 🧠 Exactly-Once vs At-Least-Once

---

### At-Least-Once

→ May process duplicates
→ Easier to implement

Requires:

* Deduplication logic

---

### Exactly-Once

→ Each record processed once
→ Harder to achieve

Requires:

* Checkpointing
* Idempotent writes
* Transactional sinks

---

## 🔁 Idempotency (REINFORCE)

→ Running same pipeline multiple times gives same result

Techniques:

* MERGE / UPSERT
* Partition overwrite
* Unique constraints
* Deduplication windows

---

## 📊 Monitoring & Observability

---

### What to Monitor?

* Job duration
* Row counts
* Failure rates
* Data freshness
* Data volume anomalies

---

### Monitoring Tools

* Airflow UI
* CloudWatch
* Stackdriver
* Custom dashboards

---

## 🚨 Alerting

→ Alerts should be:

* Actionable
* Not noisy

Trigger alerts on:

* Job failures
* SLA misses
* Data anomalies
* Missing partitions

---

## 🧠 Data Validation Layers

```
Source → Ingestion → Transformation → Serving
   |          |              |           |
   QC         QC             QC          QC
```

→ Validate at **every stage**

---

## 🧪 Data Reconciliation

→ Ensure data matches across systems

Examples:

* Source vs warehouse row count
* Daily totals comparison

---

## 🔐 Security & Data Quality

→ Bad permissions can cause:

* Missing data
* Partial loads

Ensure:

* Proper IAM roles
* Least privilege access

---

## 🧠 Interview Design Questions

* How do you ensure data quality?
* What checks do you apply in pipelines?
* How do you handle SLA breaches?
* How do you detect bad data early?
* How do you recover from failures?

---

## ✅ Chapter 30 Summary

* Data Engineers own data quality
* Quality dimensions must be enforced
* SLAs & freshness are critical
* Failures require controlled recovery
* Idempotency prevents duplicates
* Monitoring & alerting are mandatory
* Validation must exist at every stage
