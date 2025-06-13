# **V MongoDB (NoSQL Database)**

#### **Q1. Explain in detail about the Ecosystem of MongoDB with appropriate diagrams and explore collections and documents in MongoDB.**

**MongoDB Ecosystem Components:**

1. **MongoDB Server** – Core database engine.
2. **Mongo Shell** – CLI for interacting with the DB.
3. **Compass** – GUI tool to visualize and manage data.
4. **Drivers** – Connects applications (Node.js, Python, Java, etc.).
5. **Atlas** – Cloud-hosted MongoDB platform.
6. **Ops Manager** – Manages backups, automation, monitoring.
7. **Connector for BI** – Connects MongoDB to SQL-based tools.

---

**MongoDB Structure:**

* **Database** → Contains multiple **collections**
* **Collection** → Like tables, stores documents
* **Document** → JSON-like format (BSON) with key-value pairs

**Example Document:**

```json
{
  "emp_id": 101,
  "name": "Ravi",
  "dept": "Sales",
  "salary": 50000
}
```

**Diagram Tip for Exam:**

```
MongoDB Server
 └── Database (companyDB)
     └── Collection (employees)
         ├── Document 1
         ├── Document 2
         └── ...
```

---

#### **Q2. What is meant by NoSQL? Explain in detail about CRUD operations in MongoDB.**

**NoSQL (Not Only SQL):**

* Non-relational, schema-less database.
* Suited for large-scale, unstructured or semi-structured data.
* Types: Document (MongoDB), Key-Value (Redis), Column (Cassandra), Graph (Neo4j).

---

**CRUD Operations in MongoDB:**

1. **Create**

```js
db.employees.insertOne({ name: "Ravi", dept: "Sales", salary: 50000 });
```

2. **Read**

```js
db.employees.find({ dept: "Sales" });
```

3. **Update**

```js
db.employees.updateOne({ name: "Ravi" }, { $set: { salary: 60000 } });
```

4. **Delete**

```js
db.employees.deleteOne({ name: "Ravi" });
```

---

**Exam Tip Summary:**

* MongoDB uses **collections and documents**, not tables and rows.
* CRUD in MongoDB uses simple JavaScript-like syntax.
* NoSQL is **flexible**, **scalable**, and supports **high-speed data operations**.
