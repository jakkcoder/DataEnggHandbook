## 🔑 Types of Keys

→ **Candidate Key**
- A super key that contains **no extra attributes**
- Selected from the set of super keys
- Can contain **NULL values**
- One candidate key is chosen as the **Primary Key**

→ **Primary Key**
- Each relation (table) can have **only one primary key**
- Uniquely identifies each record

→ **Foreign Key**
- Used to establish a relationship between two tables
- Refers to the primary key of another table

→ **Composite Key**
- Consists of **two or more attributes**
- Used to uniquely identify rows in a table

---

## ⚙️ Scala Basics

### Concurrency vs Parallelism
- **Concurrency** → Multiple tasks in progress (context switching)
- **Parallelism** → Multiple tasks running at the same time

*(Ref: YouTube videos by Cunningham)*

---

### Object First (Scala Entry Point)

```scala
object First {
  def main(args: Array[String]): Unit = {
    println("Hello World")
  }
}
````

Notes:

* Scala is **case-sensitive**
* Used for building projects in **IntelliJ**
* Run command: `Ctrl + Fn + F10`

---

### Variables in Scala

→ `var` is used to create a variable

#### Two Types of Containers

```
        Container
        /        \
     Value      Variable
```

**Value**

* Stores fixed values
* Immutable

**Variable**

* Stores variable values
* Mutable
* Same variable can be changed without inference issues

Example:

```scala
var a = "Tanvi"
a = 5645        // ❌ will not work

var a: Any = "Tanvi"
a = 5645        // ✅ works
```

---

## 🧠 Functional Programming Concepts

* First-order functions
* Higher-order functions
* LSP (Liskov Substitution Principle)
* Dynamic Method Dispatch
* SOLID principles

---

## 🧩 `Any`, `AnyVal`, and `AnyRef`

```
                Any
               /   \
         AnyVal     AnyRef (java.lang.Object)
```

**AnyVal**

* float
* double
* int
* short
* long
* byte
* boolean
* unit
* char

**AnyRef**

* List
* Option
* User-defined classes

---

## 🧱 Scala Concepts

→ Traits in Scala are similar to **interfaces in Java**

→ **Singleton Class**

* Constructor should be private
* Only one instance exists

→ **Eager val**

* Evaluated immediately

→ **Lazy val**

* Evaluated only when needed

→ In Scala:

* The **last line is always returned**
* `return` keyword is not required

---

## 🧪 Operators & Keywords

* `instanceof`
* `hashCode`
* `String`

---

## 🗄️ Database Concepts

### Cardinality vs Ordinality

→ **Ordinality**

* Minimum number of times an instance of an entity can be associated
* Describes **parent side** of the relationship
* Can be zero

→ **Cardinality**

* Maximum number of times an instance of an entity can be associated
* Describes **child side** of the relationship

---

## 🔐 ACID Properties

ACID ensures **validity and reliability** of transactions.

* **Atomicity** → Transaction should be **all or nothing**
* **Consistency** → Database remains consistent before & after transaction
* **Isolation** → Multiple transactions can occur concurrently without conflict
* **Durability** → Data persists even if the system fails

---

## 🧱 Object

→ Object is a data structure used to **store or represent data**

---

## 📊 ER Model

To create an **ER Model**, we need to identify:

1. Entities
2. Attributes (facts about entities)
3. Relationships
4. Cardinality ratios

---

## 🐬 MySQL Basics

→ To start MySQL:

```bash
sudo mysql -u root -p
```

→ Create database:

```sql
CREATE DATABASE database_name;
```

→ Use database:

```sql
USE database_name;
```

---

## 🗑️ DROP vs TRUNCATE

→ **DROP**

* Drops table **and schema**

→ **TRUNCATE**

* Drops table data
* Schema remains intact

---

## 🧾 Data Integrity

→ Data integrity is the **consistency and accuracy of data** throughout its lifecycle.

### Types of Data Integrity

1. **Entity Integrity**

   * Enforced using:

     * Primary Key
     * Unique Constraints
     * Indexes

2. **Referential Integrity**

   * Enforced using:

     * Foreign Key
     * Primary Key constraints

3. **Domain Integrity**

   * Enforced using:

     * CHECK constraints
     * DEFAULT constraints
   * Applied at column level

Example:

* If a column has `INT` datatype, all values must be integers

---

### Constraints

→ **CHECK constraint**

* Restricts value ranges

→ **DEFAULT constraint**

* Assigns default value (e.g., system date)

---

## ⚡ Triggers

→ Database objects attached to a table
→ Automatically execute on specific events

---

## 🧠 SQL Languages

→ **DML (Data Manipulation Language)**

* INSERT
* UPDATE
* DELETE

→ **DDL (Data Definition Language)**

* CREATE
* DROP
* ALTER
* TRUNCATE
* COMMENT
* RENAME

→ **DCL (Data Control Language)**

* GRANT
* REVOKE
  *(Used for permission control)*

→ **TCL (Transaction Control Language)**

* COMMIT
* ROLLBACK
* SAVEPOINT
* SET TRANSACTION

→ Used to:

* Roll back transactions
* Define transaction characteristics
* Create save points within transactions

