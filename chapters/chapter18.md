# Structured Streaming (Advanced) & Apache Kafka – Clean Notes

---

## 🧩 Output Modes (Structured Streaming)

→ Output mode depends on **source and sink**

### Supported Output Modes

- **Append**
  → Append only **new records**
- **Update**
  → Update **changed records**
- **Complete**
  → Rewrite the **entire output**

---

## ⏱️ Event-Time Processing

### Event-Time Data

→ Event time refers to the **time embedded in the data itself**  
→ Instead of processing data based on when it **reaches the system**,
   data is processed based on **when it was generated**

---

### Watermark

→ Feature of streaming systems  
→ Defines **how late** data is expected to arrive  
→ Used to handle **late-arriving events** in event-time processing

---

# 🟦 Apache Kafka

---

## 📩 What is Kafka?

→ A **unified messaging system**  
→ Makes data pipelines **reliable, efficient, and manageable**  
→ Originally developed by **LinkedIn**

---

## 🧠 Why Kafka?

→ Used for building **real-time data pipelines**  
→ Used for **streaming applications**  
→ Highly scalable and fault-tolerant messaging system  

---

## ⚙️ Kafka Characteristics

- Scalability
- Availability
- Performance
- Zero downtime
- Extensibility (many connectors available)
- Replication

---

## 📌 When Kafka is Used

- Real-time & batch data processing
- Application logs
- Event-driven architectures

---

## 🔥 Capabilities of Kafka

→ **Publish & subscribe** to streams of records  
→ Store streams of records in a **fault-tolerant and durable** way  
→ Decouples **data producers** from **data consumers**

→ Producer speed and consumer speed can be **different**  
→ Kafka stores data until it is consumed

---

## 🌊 Kafka as a Stream

→ Kafka represents data as a **continuous stream of records**  
→ Streams are:
- Ordered
- Immutable
- Append-only

---

## 🔁 Data Flow in Kafka

→ Streaming data flows from **source → destination**  
→ Supports:
- Ingestion
- Transformation
- Distribution of streaming data

---

## 🧱 Kafka Components

### Producer (Publisher)
→ Sends messages to Kafka topics

### Consumer (Subscriber)
→ Reads messages from Kafka topics

### Broker
→ Kafka server  
→ Receives messages from producers  
→ Stores messages and serves them to consumers

---

## 🧪 Kafka Core APIs

- **Producer API**
  → Publish streams of records

- **Consumer API**
  → Subscribe to topics and consume records

- **Streams API**
  → Transform streams of data  
  → Used for **bigger transformations**

- **Connector API**
  → Kafka Connect  
  → Push data to/from external systems

---

## 🔌 Kafka Connect

→ Used to move data **between Kafka and external systems**  
→ Useful when:
- Data needs to be pushed after a specific time
- External systems need Kafka data

---

## 🔄 Kafka Streams API

→ Allows an application to:
- Consume from one or more topics
- Process the stream
- Produce results to one or more output topics

---

## 🌐 Language & Communication

→ Kafka communication happens over **language-agnostic TCP protocol**  
→ Language does **not matter** (Java, Python, etc.)

---

# 📤 Producer API (Detailed)

---

## 👤 Who Can Be a Producer?

Examples:
- Web servers publishing click events
- Log scrubbers pushing log messages
- Sensors pushing telemetry data

---

## 🔁 Producer Characteristics

- Multiple concurrent producers can write to the same topic
- Producer must specify a **message key** (e.g., `Cust_ID`)
- Messages are serialized into **byte arrays**

---

## 📡 Publishing Options

```

Publishing Options
/          
Synchronous   Asynchronous

```

### Synchronous
→ Producer waits for **acknowledgement**

### Asynchronous
→ Producer does **not wait** for acknowledgement

---

## ❓ What Does a Producer Publish?

→ Publishes a **stream of data** to Kafka cluster  

Terminology:
- Published data = **Message**
- Message is published to a **Topic**
- Message is also called an **Event**

---

### Message Definition

→ A message represents a **record of a real-world event**  
→ Captured at a **particular point in time**

Example:
- User clicked a button
- Sensor reported temperature

---

## ✅ Summary

- Structured Streaming supports append, update, and complete modes
- Event-time processing handles late data using watermarks
- Kafka is a scalable, fault-tolerant messaging system
- Producers publish events; consumers subscribe to topics
- Kafka decouples data producers from consumers
- Communication is language-agnostic
