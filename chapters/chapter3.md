# Data Warehouse & ETL – Clean Notes

---

## 🏢 Data Warehouse

### Transactional Processing (OLTP)
→ Analyzes **individual entities**
→ Accesses **recent data** (hours or days)
→ Supports **real-time access**
→ Usually works on a **single data source**
→ Focused on **updates and inserts**

---

### Analytical Processing (OLAP)
→ Analyzes **large batches of data**
→ Covers **months or years**
→ Long-running queries
→ Reads historical data
→ Works with **multiple data sources**

---

### Data Warehouse Definition

→ A **subject-oriented**, **integrated**, **time-variant**, and **non-volatile** collection of data  
→ Used to support **management decision-making**  
→ This process is called **Data Warehousing**

#### Key Characteristics

→ **Subject-Oriented**
- Built around business subjects like:
  - Customers
  - Sales
  - Products

→ **Integrated**
- Data collected from **multiple sources**
- Converted into a **consistent format**

→ **Time-Variant**
- Stores **historical data**
- Enables trend analysis

→ **Non-Volatile**
- Once data is stored, it is **not updated or deleted**
- Read-only for analysis

---

## ❓ Need for Data Warehouse

- Multiple data sources → synchronization required
- Data analysis becomes easier
- RDBMS is **not optimized** for analytical processing
- No single system of records in OLTP
- Enables **balanced and accurate analysis**

---

## ⚙️ Operational vs Informational Systems

### Operational System
→ Runs business in **real time**
→ Based on **current data**
→ Also called **OLTP (Online Transaction Processing)**

### Informational System
→ Supports **managerial decision-making**
→ Uses **historical and predictive data**
→ Also called **OLAP (Online Analytical Processing)**

---

## 🆚 OLTP vs OLAP

| Feature | OLTP | OLAP |
|------|------|------|
| Users | Clerks, Salespersons | Managers, Business Analysts |
| Query Type | Narrow, simple | Broad, complex |
| Updates | Frequent, small updates | Periodic batch updates |
| Data Volume | Few rows | Many or all rows |

---

## 🔄 ETL (Extract, Transform, Load)

```

Source Systems
↓
Staging Area
↓
Transform
↓
Data Warehouse
↓
Data Marts
↓
Visualization (Tableau, Power BI)

```

---

### ETL Explanation

→ Data is first brought into a **staging area**
→ Data from different sources is converted into the **same format**
→ Transformation cleans, standardizes, and enriches the data

---

### Extract
→ Pulling expected data from different sources into a common staging area

**Sources can be:**
- Flat files (CSV, delimited files)
- RDBMS systems
- Mainframe files / DB2 databases
- XML / JSON files

---

### Transform
→ Altering data based on **business rules**
- Data type conversion
- Date format standardization
- Name concatenation (first + last name)
- Data cleansing

---

### Load
→ Loading transformed data into the **target system**
- Data Warehouse
- Data Marts

---

## 🏗️ Data Warehouse Architecture

### Architecture Types

→ Without staging area  
- Data transformed directly into the warehouse  
- Minimal transformation

→ With staging area  
- Data cleaned and transformed before loading

→ Architecture with Data Marts  

---

## 📦 Data Mart

→ A **subset of a data warehouse**
→ Department-specific or domain-specific
→ Improves query performance
→ Reduces data volume
→ Implements access control strategies

**Characteristics**
- Highly denormalized
- Restrictive
- Project-oriented
- Short life cycle
- Built based on use case

---

## 📊 Data Warehouse Tables

### Dimension Table
→ Describes **business entities**
→ Contains descriptive attributes
→ Used for analysis

Example:
- Customer ID
- Customer Name
- Location

---

### Fact Table
→ Stores **quantitative data**
→ Transactional information
→ Contains:
- Measurements
- Metrics
- Foreign keys to dimension tables

---

### Usage
→ Fact and Dimension tables together support **analytics & decision-making**

Example:
- Customer table → Dimension table
- Customer transactions → Fact table

---

## 🧩 Data Warehouse Schemas

### Star Schema
→ Looks like a star  
→ One **fact table** in the center  
→ Multiple **dimension tables** around it  
→ Dimension tables are **denormalized**

```

```
 Dimension
    |
```

Dimension — Fact Table — Dimension
|
Dimension

```

---

### Snowflake Schema
→ Dimension tables are **normalized**
→ More number of tables
→ Reduced redundancy
→ Increased complexity

---

### Fact Constellation (Galaxy Schema)
→ Multiple fact tables
→ Shared dimension tables
→ Used for complex analytics

---

## ⚖️ Performance Comparison

- **Star Schema** → Better query performance
- **Snowflake Schema** → Saves space, slower queries
- **Fact Constellation** → Complex but powerful

---

## 🔄 Slowly Changing Dimensions (SCD)

→ Dimensions that change **slowly over time**

### Types of SCD

→ **Type 0**
- Dimension attributes never change
- Fixed dimension

→ **Type 1**
- No history maintained
- Old value replaced with new value

→ **Type 2**
- Full history maintained
- Multiple records for same natural key
- Versioning used

→ **Type 3**
- New attribute added
- Stores limited history (current + previous)

→ **Type 4**
- History maintained in a separate table

→ **Type 6 (Hybrid)**
- Combination of Type 1, 2, and 3
- Used based on business requirements

---
