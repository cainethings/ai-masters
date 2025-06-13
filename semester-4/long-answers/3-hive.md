# **III. Hive (Data Warehousing)**

---

#### **Q1. What are the different types of joins in Hive? Explain with appropriate example for each.**

Hive supports four main types of joins:

---

**1. Inner Join**
Returns only matching rows between two tables.

```sql
SELECT a.id, b.name 
FROM emp a 
JOIN dept b ON a.dept_id = b.dept_id;
```

---

**2. Left Outer Join**
Returns all rows from the left table and matching rows from the right; unmatched right rows return NULL.

```sql
SELECT a.id, b.name 
FROM emp a 
LEFT OUTER JOIN dept b ON a.dept_id = b.dept_id;
```

---

**3. Right Outer Join**
Returns all rows from the right table and matching rows from the left.

```sql
SELECT a.id, b.name 
FROM emp a 
RIGHT OUTER JOIN dept b ON a.dept_id = b.dept_id;
```

---

**4. Full Outer Join**
Returns all rows from both tables with NULLs where there’s no match.

```sql
SELECT a.id, b.name 
FROM emp a 
FULL OUTER JOIN dept b ON a.dept_id = b.dept_id;
```

---

**Note for Exam**:
Use **emp** and **dept** table as common examples; always state that join condition is on a shared key (like `dept_id`).

---

#### **Q2. Implement HQL partitioning and bucketing using Hive for employee databases.**

---

**Partitioning:**
Used to divide table data into parts based on column values (e.g., department, year).

```sql
CREATE TABLE emp_part (
  id INT, 
  name STRING, 
  salary FLOAT
) 
PARTITIONED BY (dept STRING)
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY ',';
```

**Load data into a partition:**

```sql
LOAD DATA INPATH '/user/data/emp_sales.csv' 
INTO TABLE emp_part 
PARTITION (dept='Sales');
```

---

**Bucketing:**
Distributes data into fixed number of files based on hash of a column (e.g., employee ID).

```sql
CREATE TABLE emp_bucket (
  id INT, 
  name STRING, 
  salary FLOAT
) 
CLUSTERED BY (id) INTO 4 BUCKETS;
```

**Note:** Requires `SET hive.enforce.bucketing=true;` before inserting data.

```sql
INSERT OVERWRITE TABLE emp_bucket 
SELECT * FROM emp;
```

---

**Summary Tip for Exam:**

* **Partitioning** = Folder-level segregation (efficient filtering)
* **Bucketing** = Hash-based splitting (efficient joins & sampling)
* Mention practical columns like **`dept`, `year`, `id`** for clarity.
