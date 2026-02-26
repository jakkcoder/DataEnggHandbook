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

**Concurrency** means you are doing **many things**, but **one at a time** by switching quickly.

**Parallelism** means you are doing **many things at the exact same time**.

#### Super simple examples

- **Single-lane road vs multi-lane road**
  - **Concurrency**: one lane. Many cars *share* the lane by taking turns.
  - **Parallelism**: multiple lanes. Cars move side-by-side at the same time.

- **One person vs two people**
  - **Concurrency**: one person cooks dinner and answers messages by switching: cook → reply → cook → reply.
  - **Parallelism**: two people: one cooks while the other replies. Both happen at the same time.

- **Computer example**
  - **Concurrency**: 1 CPU core runs Task A for a tiny slice of time, then Task B, then back to A (time-slicing).
  - **Parallelism**: 2+ CPU cores run Task A and Task B at the same time.

**Easy memory line:** Concurrency = *taking turns*. Parallelism = *at the same time*.

#### Python examples

**Concurrency (asyncio)**: tasks overlap by *waiting* (great for I/O like network calls).

```python
import asyncio

async def task(name: str, seconds: int):
    print(f"start {name}")
    await asyncio.sleep(seconds)  # waiting (doesn't block the whole program)
    print(f"done  {name}")

async def main():
    await asyncio.gather(
        task("A", 2),
        task("B", 1),
    )

asyncio.run(main())
```

**Parallelism (multiprocessing)**: tasks run on *multiple CPU cores* (good for CPU-heavy work).

```python
from multiprocessing import Process
import time

def work(name: str):
    print(f"start {name}")
    time.sleep(2)  # imagine heavy CPU work here
    print(f"done  {name}")

if __name__ == "__main__":
    p1 = Process(target=work, args=("A",))
    p2 = Process(target=work, args=("B",))
    p1.start(); p2.start()
    p1.join();  p2.join()
```

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

**Ordinality (minimum)** = *What is the minimum number of related records allowed?*\n
**Cardinality (maximum)** = *What is the maximum number of related records allowed?*\n
Think: **min..max**.

#### Example (easy): Customers and Orders

Tables:

```text
Customers
customer_id | name
1           | Asha
2           | Ben
3           | Chen

Orders
order_id | customer_id | amount
101      | 1           | 25
102      | 1           | 40
103      | 2           | 10
```

Relationship: **Customer → Order**

- **Ordinality (min) on Customer side**: can a customer have *zero* orders?
  - If yes (common), then **Customer has 0..** orders (minimum is 0).
  - If no (rare), then **Customer has 1..** orders (minimum is 1).

- **Cardinality (max) on Customer side**: what’s the maximum orders a customer can have?
  - Usually unlimited → **0..N** (or **1..N**).

- **Order side** (typical rule): each order belongs to exactly one customer → **1..1**.
  - Minimum 1 (must have a customer), maximum 1 (only one customer).

So a common real-world constraint looks like:

→ **Customer** has **0..N** Orders  
→ **Order** belongs to **1..1** Customer

---

## 🔐 ACID Properties

ACID ensures **validity and reliability** of transactions.

Think of a **transaction** as a “package of steps” that must behave safely.

### Layman example: Bank transfer (₹500 from Asha → Ben)

Steps inside one transaction:
1. Deduct ₹500 from Asha
2. Add ₹500 to Ben

#### A — Atomicity (all or nothing)
If step 1 succeeds but step 2 fails, we must **undo step 1**.\n
So either **both happen** or **none happen** (no “money lost in between”).

#### C — Consistency (rules must stay true)
The database must never break rules like:
- balance can’t go negative (if your system enforces that)
- total money doesn’t randomly change

After the transfer, the data must still make sense according to constraints.

#### I — Isolation (transactions don’t step on each other)
If two transfers happen at the same time, they shouldn’t interfere.\n
Example: Asha has ₹600 and two transfers try to send ₹500 at the same time.
- Without isolation, both might read ₹600 and both might succeed (wrong).
- With isolation, the database ensures the result is correct (only one succeeds or they run in a safe order).

#### D — Durability (once committed, it stays)
After the transaction says “SUCCESS”, the result is saved permanently.\n
Even if the server crashes right after, the transfer should still be there when the database comes back.

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

