# Apache Spark – Null Handling, Complex Types & Data Sources – Clean Notes

---

## 🧩 Date & Utility Functions

→ Functions that are **not registered** cannot be used directly  
→ Return type should always **match the column type**

Common functions:
- `datediff()` → Difference between two dates
- `to_date()` → Convert string to date

---

## 🚫 Null Handling in Spark

→ Presence of **null / empty values** makes optimization difficult in Spark  
→ Spark uses `na` package to handle missing values

### Two Ways to Handle Nulls

1. Explicitly **drop** nulls  
2. **Fill** null values

---

### Common Null Functions

→ **coalesce**
- Picks the **first non-null value** from a set of columns

→ **drop**
- Removes rows that contain null values

→ **fill**
- Fills one or more columns with specified values

→ **replace**
- Similar to regular expression replacement

---

## 🧬 Complex Data Types

### Struct
→ DataFrame inside a DataFrame  
→ Access fields using:
- Dot notation
- `getField()`

---

### Array
→ Collection of elements of the **same data type**

Useful functions:
- `split()`
- `array_length()` / `size()`
- `array_contains()`
- `explode()`

---

### Map
→ Key–value pairs  
→ Created using `create_map()`

---

## 👤 User Defined Functions (UDF)

→ UDFs can be written in **any supported language**  
→ Must be **registered** before use  
→ Can be reused across different Spark languages

---

## 📥 Data Sources in Spark

Spark supports **all types of data**:

### Structured
- JDBC / ODBC connections

### Semi-Structured
- CSV
- JSON
- Parquet
- ORC

### Unstructured
- Plain text files

---

### Common External Sources

- Cassandra
- MongoDB
- HBase
- XML
- Redshift
- AWS (S3)

→ Spark provides built-in connectors to import data from these sources

---

## 📖 Read API Structure

→ Spark uses **DataFrameReader** to read data

Key components:
- **Format**
- **Schema**
- **Read Mode**
- **Options** (format-specific)

---

### Read Modes

Spark supports **three read modes**:

1. **Permissive** (default)
   - Corrupt records are set to `null`
   - New column created for corrupt data

2. **DropMalformed**
   - Corrupt records are dropped

3. **FailFast**
   - Fails immediately
   - No DataFrame is created

---

## ✍️ Write API Structure

→ Spark uses **DataFrameWriter** to write data

Components:
- Format (`text`, `csv`, `json`, etc.)
- Save Mode
- Options

---

### Save Modes

- **append** → Appends data
- **overwrite** → Overwrites existing data
- **errorIfExists** → Throws error if data exists
- **ignore** → Ignores write if data exists

---

## 📄 Semi-Structured Data: CSV Files

→ CSV = Comma Separated Values  
→ Each line represents one record  
→ Comma separates fields

---

### CSV Options

| Read / Write | Key |
|--------------|-----|
| Both | `sep` |
| Both | `header` |
| Read | `escape` |
| Read | `inferSchema` |
| Read | `ignoreLeadingWhiteSpace` |

---

## ⚠️ Failures While Reading CSV Files

Common issues:
- Schema mismatch
- File name mismatch
- File does not exist

---

## 💾 Writing CSV Files

Example:
```python
df.write \
  .format("csv") \
  .mode("overwrite") \
  .option("header", "true") \
  .save("path/to/output")
