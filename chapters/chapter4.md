# ETL, Big Data & Hadoop Fundamentals – Clean Notes

---

## 🔧 ETL & Scheduling Tools

### ETL Tools
- Talend
- Informatica
- IBM DataStage

### Scheduling Tools
- Autosys
- Tidal
- Control-M

---

## 🔄 Data Loading Types

→ **Historical / Initial Load**
- Used when a data warehouse is created for the first time
- Loads complete historical data

→ **Incremental Load**
- Loads only newly added data
- Usually runs:
  - Daily
  - Weekly
  - Fortnightly

---

## 📊 Big Data

### Sources of Data
- Machines
- People
- Organizations

### Emergence of Big Data
- All the **V’s**
- Cloud computing (computing anywhere)
- Advanced hardware

---

### Challenges in Big Data

- Machine-generated data → complex
- Human-generated data → unstructured
- Organization-generated data → stored in silos

---

### Big Data Definition

→ Big data refers to a **huge amount of structured, semi-structured, and unstructured data**  
→ Cannot be stored or processed using traditional databases

---

### The 5 V’s of Big Data

→ **Volume**
- Size of the data generated and stored

→ **Velocity**
- Speed at which data is generated and accessed

→ **Variety**
- Structured (tables)
- Semi-structured (JSON, XML)
- Unstructured (images, videos)

→ **Veracity**
- Accuracy and reliability of data

→ **Value**
- How useful the data is for decision-making

---

## 🐘 Hadoop Ecosystem

→ A **platform / suite** that provides various services to handle big data  
→ Consists of multiple tools working together

---

## 📂 Distributed File System

→ Distributes files **across multiple machines** over a network  
→ Enables fault tolerance and scalability

---

## 🧩 Commodity Cluster

→ An ensemble of **fully independent computing systems**
→ Integrated using **commodity hardware** over a network

### Characteristics
- **Affordable** → Easy to procure
- **Scalable** → Capacity can be increased
- **Flexible** → Can scale up or down

---

## 🎯 Central Theme of Big Data

→ **Distributed Storage**
- Data stored across multiple systems

→ **Distributed Processing**
- Code is sent to where data resides
- Avoids moving large data to computation nodes
- Based on **data locality**

Reasons:
1. Computation is parallelized
2. Multiple processors handle data efficiently

---

## 🧠 Distributed Processing Model

→ Distributed processing is achieved through a **programming model**

→ Programming model consists of:
- Runtime libraries
- Interfaces
- High-level and low-level languages

---

## 🧪 Programming Model Requirements for Big Data

→ Programmability over distributed file systems

### Requirements
1. Support big data operations
2. Handle fault tolerance
3. Support adding more nodes
4. Optimized for specific data types

---

## ⚙️ Big Data Operations

1. Split volumes of data
2. Access data fast
3. Distribute computations to nodes

---

## 🛡️ Fault Tolerance

→ Achieved by:
1. Replicating data partitions
2. Recovering files when needed

---

## ➕ Adding More Nodes (Scalability)

### Scaling Out
- Adding more machines (nodes)
- System continues to work efficiently

### Vertical Scaling (Scaling Up)
- Increasing capacity of a single system
- Adding more CPU, memory, or storage

### Horizontal Scaling (Scaling Out)
- Connecting more systems together
- Cost-effective
- Preferred for big data systems

---

## ⚡ Optimized for Specific Data

→ Optimization means achieving results:
- With minimal resources
- In minimal time

→ Programming model is designed for **huge data volumes**

⚠️ Not all programming models work for all types of data

---
