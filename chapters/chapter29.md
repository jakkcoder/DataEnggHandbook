# Workflow Orchestration with Apache Airflow (Chapter 29)

---

## 🎯 Why Orchestration Matters

→ Data pipelines are **not single jobs**  
→ They are **multiple dependent tasks**

Airflow helps:
- Schedule jobs
- Manage dependencies
- Handle retries
- Monitor failures

⚠️ Airflow does NOT process data  
→ It **orchestrates** processing tools (Spark, SQL, Python, etc.)

---

## 🧭 What is Apache Airflow?

→ Open-source workflow orchestration platform  
→ Uses **DAGs (Directed Acyclic Graphs)**  
→ Written in **Python**

---

## 🧩 DAG (Directed Acyclic Graph)

```

Task A → Task B → Task C

````

Rules:
- Directed (one direction)
- Acyclic (no loops)

→ DAG defines:
- Tasks
- Dependencies
- Schedule

---

## 🧠 Core Airflow Components

---

### Scheduler
→ Decides **when** tasks should run  
→ Monitors DAG schedules

---

### Web Server
→ Provides **UI**
→ Used for:
- Monitoring
- Triggering DAGs
- Debugging

---

### Executor
→ Defines **how tasks are executed**

Types:
- SequentialExecutor
- LocalExecutor
- CeleryExecutor
- KubernetesExecutor

---

### Metadata Database
→ Stores:
- DAG states
- Task instances
- Execution history

---

### Worker
→ Executes tasks assigned by executor

---

## 🧱 Tasks in Airflow

→ Smallest unit of work  
→ Represent a single action

Examples:
- Run Spark job
- Execute SQL
- Call API
- Run Python script

---

## ⚙️ Operators

→ Operators define **what a task does**

Common operators:
- `PythonOperator`
- `BashOperator`
- `SparkSubmitOperator`
- `BranchPythonOperator`
- `EmailOperator`

---

## 🔍 Sensors

→ Sensors **wait for a condition**

Examples:
- File arrival
- Table update
- API response

Common sensors:
- `FileSensor`
- `ExternalTaskSensor`
- `S3KeySensor`

⚠️ Sensors can be expensive if not used carefully

---

## 🔁 Scheduling Concepts

---

### Schedule Interval

→ Defines **how often** DAG runs

Examples:
- `@daily`
- `@hourly`
- Cron expressions

---

### Start Date

→ Date from which DAG becomes active  
→ Important for **backfills**

---

### Catchup

→ Controls whether **past runs** should execute

```python
catchup=False
````

---

## 🔄 Backfills in Airflow

→ Running DAGs for **past dates**

Used when:

* Pipeline was down
* Logic was fixed
* Data arrived late

⚠️ Backfills must be used carefully to avoid overload

---

## 🔁 Retries & Failure Handling

→ Tasks can fail due to:

* Network issues
* Temporary outages
* Resource limits

Airflow supports:

* Retry count
* Retry delay
* Exponential backoff

---

## ⏱️ SLA (Service Level Agreement)

→ Defines **expected execution time**

Example:

* Task must finish within 30 minutes

If SLA missed:

* Alerts triggered
* Logged for monitoring

---

## 🚨 Alerting & Monitoring

→ Airflow supports:

* Email alerts
* Slack alerts
* Custom callbacks

→ Alerts can be triggered on:

* Task failure
* SLA miss

---

## 🧠 Idempotency in Airflow

→ DAGs may be retried or rerun
→ Tasks must be **idempotent**

Techniques:

* Use partition-based loads
* Avoid partial writes
* Use UPSERT / MERGE

---

## 🧪 Dependency Management

→ Task dependencies defined using:

```python
task_a >> task_b
```

or

```python
task_b.set_upstream(task_a)
```

---

## 🔐 Connections & Variables

→ Used to store:

* Credentials
* Environment configs

Benefits:

* No hardcoding
* Secure
* Reusable

---

## ⚡ Best Practices (INTERVIEW GOLD)

* Keep tasks **small**
* Avoid long-running tasks
* Use sensors carefully
* Set retries wisely
* Make tasks idempotent
* Avoid heavy logic in DAG file
* Separate business logic from orchestration

---

## 🧠 Common Interview Questions

* What is a DAG?
* How does Airflow differ from Spark?
* How do retries work?
* How do you handle backfills?
* How do you prevent duplicate data?
* What is the role of sensors?

---

## ✅ Chapter 29 Summary

* Airflow orchestrates, not processes
* DAG defines tasks & dependencies
* Operators execute tasks
* Sensors wait for conditions
* Retries & SLAs improve reliability
* Idempotency is critical
* Backfills must be controlled
