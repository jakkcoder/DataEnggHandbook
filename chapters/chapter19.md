# Apache Kafka – Messages, Topics, Partitions, Brokers & Consumers (Clean Notes)

---

## 📩 Kafka Messages

→ Kafka treats **each message as an array of bytes**  
→ **Size limit exists** for a message in Kafka  
→ Default maximum message size is **1 MB**, but it is **configurable**
  (can be increased or decreased)

---

## 🧾 Message Content

A Kafka message contains:

- **Key**
  → Defined by the producer  
  → Optional (not mandatory)

- **Value**
  → Actual message content  
  → Stored as a **byte array**  
  → Semantics are decided by the producer / consumer

- **Timestamp**
  → Time at which the message is produced

- **Headers**
  → Optional metadata

---

### Event Time vs Ingestion Time

- **Event Time**
  → Time at which the message is produced

- **Ingestion Time**
  → Time at which the Kafka broker timestamps the data  
  → Time when data is ingested into the Kafka cluster

---

### Messages Without Key

→ If a message does **not have a key**, Kafka **automatically generates a key**

---

## 🧵 Kafka Topics

→ Producers can publish messages to **multiple topics**  
→ Consumers can consume messages from **multiple topics**

→ **Topic**
- Logical entity that holds messages
- Identified by a **unique name**
- Records are published to topics

Analogies:
- Topic ≈ table with records
- Topic ≈ queue for similar messages

→ Similar producers publish messages to the same topic  
→ Similar consumers consume messages from that topic

---

## 👥 Topic Subscription Model

→ Topics in Kafka are **multi-subscriber by default**

A topic can have:
- Zero consumers
- One consumer
- Many consumers

---

## 🧩 Partitions

```

Group of messages  → Partition
Group of partitions → Topic

```

→ Partitioning is a **physical concept**  
→ Partitions allow Kafka to:
- Scale horizontally
- Support parallelism

---

## 📥 Consumer API

→ A consumer is an application that **reads data from Kafka cluster**

Examples:
- Log file readers
- Real-time aggregators
- Data archivers

---

## 🔀 Ways to Consume Data

```

Consume
/        
Batch     Streaming

```

### Batch
→ Producer publishes data  
→ Consumer consumes data **at its own pace**

### Streaming
→ Data is consumed **as soon as it is produced**

---

## 📌 Offset Management

→ Consumers manage the **offset** of the data  
→ Offset decides **from where** a consumer starts reading

→ Consumers can:
- Start from a specific offset
- Resume from last committed offset

→ Consumers must send **acknowledgement** to the broker

---

## 🧱 Kafka Broker

→ Kafka is essentially a **broker-based system**  
→ Broker is the **brain of Kafka**

Responsibilities of a broker:
- Receives messages from producers
- Stores messages locally in **logs**
- Keeps track of active consumers
- Maintains heartbeat with consumers
- Manages topic partitions
- Manages lifecycle of topics

→ **Multiple brokers together form a Kafka cluster**

---

## 📂 Logs in Kafka

→ Producers send data to Kafka cluster  
→ Logs store data **event by event** from producers  

Characteristics:
- Logs are **physical files**
- Managed by Kafka brokers
- Each broker has an assigned **log directory**
- Logs are **opened periodically**
- Old data is **pruned or flushed** after a configured number of days

---

## 🧱 Partitions (Detailed)

→ Partition = ordered, immutable sequence of records  
→ Continuously appended

Key points:
- Each topic can have **one or more partitions**
- Number of partitions is defined during topic creation
- Increasing partitions improves **scalability**
- Each partition has its **own physical log file**

---

### Writing to a Partition

→ When a producer writes a message:
- Message is sent to the **leader broker** of that partition
- Leader handles log updates

→ Each published message:
- Is written to **only one partition**
- For fault tolerance, partitions are **replicated**
- Replicas are stored on **other brokers**

→ **Message ordering is guaranteed within a partition**

---

## 🔢 Partition Assignment

→ Kafka uses a **hashing function** to decide partition placement  
→ Kafka does **not** create partitions dynamically

---

## 👥 Consumer Groups

→ When data volume is high and a single consumer is slow:
- Multiple consumers are grouped together

→ **Consumer Group**
- Single logical unit
- Shares the workload of a topic

Rules:
- Each message is sent to **only one consumer** in a group
- Each partition is consumed by **only one consumer** in a group

---

## 🔄 Load Rebalancing

→ Kafka brokers track consumers  
→ If a consumer goes down:
- Kafka **rebalances partitions**
- Workload is redistributed among remaining consumers

---

## 🧮 Offset Management (Detailed)

→ Mechanism to track:
- Which messages are delivered
- Which messages are yet to be processed

→ This mechanism is called **Offset Management**

→ Consumers are responsible for:
- Maintaining
- Committing
- Managing offsets

---

## ✅ Summary

- Kafka messages are byte arrays with optional keys and headers
- Topics logically group similar messages
- Partitions enable scalability and parallelism
- Brokers store data in logs and manage cluster state
- Consumer groups share workload efficiently
- Offsets track consumption progress
- Load rebalancing ensures fault tolerance
