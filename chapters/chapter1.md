---

# Linux & Database Fundamentals – Clean Notes

---

## 1. Linux Basics & Directory Navigation

### Common Directories

* **Root directory (`/`)** – Top-level directory in Linux
* **Home directory (`~`)** – User’s personal directory
* **Current directory (`.`)** – Present working directory
* **Parent directory (`..`)** – One level up from the current directory
* **Previous directory (`-`)** – Last visited directory

### File & Directory Colors (Terminal)

* **Green** → Executable files
* **Blue** → Directories
* **Black** → Regular files
* **Hidden files** → Start with `.` (dot)

---

## 2. Navigation Commands

### `cd` – Change Directory

Used to navigate between directories.

```bash
cd dir_name
cd ..
cd ../..
```

---

## 3. Listing Files & Directories (`ls`)

### Basic Usage

* `ls` → Lists files and directories
* `ls -a` → Shows all files, including hidden files
* `ls -l` → Long listing (permissions, size, owner, date)
* `ls -t` → Sort by modification time (newest first)
* `ls -lt` → Long listing sorted by time
* `ls -lr` → Reverse alphabetical order
* `ls -R` → Recursively lists files in subdirectories

---

## 4. Searching Text (`grep`)

Searches for patterns inside files.

```bash
grep "word" file.txt
grep "pattern" *.txt
```

---

## 5. File & Directory Creation

### `touch`

* Creates an empty file
* Updates timestamp of an existing file

```bash
touch file1.txt
```

### `mkdir`

* Creates directories

```bash
mkdir dir1
mkdir dir1 dir2 dir3
```

---

## 6. Removing Files & Directories

### `rmdir`

* Removes **empty directories only**

```bash
rmdir dir1
```

### `rm`

* Deletes files or directories

```bash
rm file1.txt
rm -R dir1   # Removes non-empty directory recursively
```

---

## 7. Copying Files & Directories (`cp`)

```bash
cp file1 file2           # Copy file
cp file1 dir1            # Copy file into directory
cp -R dir1 dir2          # Copy directory recursively
```

---

## 8. Moving & Renaming (`mv`)

```bash
mv file1 file2           # Rename file
mv file1 dir1            # Move file to directory
```

> `mv` works for both files and directories and is similar to cut-paste.

---

## 9. Viewing & Combining Files (`cat`)

### Concatenate files

```bash
cat file1.txt file2.txt
```

### Redirect output

* `>` → Overwrite

```bash
cat file1.txt > file2.txt
```

* `>>` → Append

```bash
cat file1.txt >> file2.txt
```

### Combine files into a third file

```bash
cat file1.txt file2.txt >> file3.txt
```

---

## 10. Disk Usage (`du`)

* `du file.txt` → Disk usage
* `du -h file.txt` → Human-readable format

---

## 11. Data & Metadata Concepts

### Example

| Name  | Age  | Rating  |
| ----- | ---- | ------- |
| name1 | age1 | rating1 |
| name2 | age2 | rating2 |

* **Data** → Actual values (rows)
* **Metadata** → Structure/schema (column definitions)

---

## 12. Database Basics

* **Database**: A collection of related data and metadata, organized for efficient storage and retrieval.
* **Tables** → Relations / Entities
* **Rows** → Tuples / Records
* **Columns** → Attributes

---

## 13. Data Warehouse

* Aggregates data from **multiple sources**
* Used for **analytics & business intelligence**
* Introduced because traditional databases were **not optimized for analytical workloads**

---

## 14. MDM (Master Data Management)

* Organizational-level system for **managing and maintaining core business data**
* Ensures data consistency across systems

---

## 15. Keys in Databases

### Super Key

* A **single attribute or set of attributes** that uniquely identifies a record
* Most general type of key
* May contain **NULL values**

---
