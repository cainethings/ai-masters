# **Unit 3: Data Ingestion (Sqoop & Flume)**

## 2 Marks
### Q1. Compare sqoop and flume
- **Sqoop** is used for importing/exporting data between **RDBMS and Hadoop**.
- **Flume** is used for **real-time ingestion** of streaming/log data into Hadoop.
- Sqoop works best for **structured, batch-based data**.
- Flume is ideal for **event-driven, unstructured or semi-structured data**.
- Sqoop connects to **databases**; Flume connects to **data sources like logs, Twitter, etc.**

### Q2. How can we control the number of mappers using sqoop?
- Use the option `--num-mappers` or shorthand `-m` in the Sqoop command.   
- Default is **4 mappers**.   
- To control parallelism or reduce load, set it manually (e.g., `--num-mappers 1`).  
- Useful when importing small tables or when splitting is not feasible.
- **Example:** ```sqoop import --connect jdbc:mysql://localhost/db --table employees --num-mappers 2```

## 16 Marks
### Q1. Explain in detail about data ingestion tools available in big data and how the data’s are ingested into the model.

#### 🔹 **What is Data Ingestion?**
- It is the process of collecting and transferring data from various sources to a storage or processing system.
- Sources include databases, logs, sensors, social media, cloud, APIs, etc.
- Can be **batch-based** or **real-time (streaming)**.

#### 🔹 **Types of Data Ingestion**
- **Batch Ingestion** – Large volumes of data moved at intervals (e.g., daily, hourly).
- **Real-Time Ingestion** – Data is ingested continuously as it is generated.


#### 🔹 **Popular Data Ingestion Tools in Big Data**

##### 1. **Apache Sqoop**
- Transfers **structured data** from **RDBMS** to **HDFS, Hive, or HBase**.
- Works in **batch mode**.
- Supports **import** and **export** operations.
- Ideal for **enterprise databases** like MySQL, Oracle, PostgreSQL.

##### 2. **Apache Flume**
- Designed to ingest **real-time, unstructured data** (e.g., logs, events).
- Suitable for **streaming data** from web servers or social media.
- Supports custom sources, channels, and sinks.
- Moves data into HDFS or HBase.

##### 3. **Apache Kafka**
- Distributed messaging system used for **real-time streaming ingestion**.
- Handles **high throughput** of messages.
- Acts as a **buffer** between producers and consumers.

##### 4. **NiFi**
- Web-based interface for building **data flow pipelines**.
- Supports real-time data routing, transformation, and system mediation.

#### 🔹 **How Data Is Ingested into Big Data Models**

- **Step 1: Connect to Data Sources**
  - Tools like Sqoop connect to **databases**, Flume to **log/event sources**, and Kafka to **message producers**.

- **Step 2: Ingest Data into Hadoop Ecosystem**
  - Data is pushed into **HDFS**, **Hive**, or **HBase** for storage.

- **Step 3: Processing with Tools**
  - Tools like **Spark**, **MapReduce**, or **HiveQL** process the ingested data.

- **Step 4: Load into Models**
  - Cleaned and processed data is used to **train machine learning models** or for **data analysis**.

#### 🔹 **Example Use Case (Elaboration)**

> Suppose an e-commerce website wants to analyze customer behavior:
- **Flume** collects real-time clickstream data from web servers.
- **Sqoop** imports customer profile data from MySQL into Hive.
- Data is processed using **Spark SQL**.
- Final dataset is used to build a **recommendation model**.


### Q2. Elaborate in detail about the steps for extracting twitter data using flume.

#### 🔹 **What is Flume?**
- A distributed, reliable, and available system for efficiently collecting, aggregating, and moving **large amounts of streaming data** into Hadoop.
- Ideal for **log and event data ingestion**.

#### 🔹 **Steps to Extract Twitter Data using Flume**

##### 1. **Register a Twitter Developer Account**
- Create a project and app on the [Twitter Developer Portal](https://developer.twitter.com).
- Get the **API key, API secret, Access token, and Access token secret**.

##### 2. **Configure Flume with Twitter Source**
- Create a **Flume configuration file** (e.g., `twitter.conf`).
- Define:
  - **Source**: Twitter (using OAuth credentials).
  - **Channel**: Memory or File Channel.
  - **Sink**: HDFS or console.

##### 3. **Sample `twitter.conf` file**
```properties
agent1.sources = twitter-source
agent1.channels = memory-channel
agent1.sinks = hdfs-sink

agent1.sources.twitter-source.type = org.apache.flume.source.twitter.TwitterSource
agent1.sources.twitter-source.consumerKey = <API_KEY>
agent1.sources.twitter-source.consumerSecret = <API_SECRET>
agent1.sources.twitter-source.accessToken = <ACCESS_TOKEN>
agent1.sources.twitter-source.accessTokenSecret = <ACCESS_TOKEN_SECRET>
agent1.sources.twitter-source.keywords = bigdata,hadoop

agent1.sinks.hdfs-sink.type = hdfs
agent1.sinks.hdfs-sink.hdfs.path = hdfs://localhost:9000/user/flume/tweets/

agent1.channels.memory-channel.type = memory

agent1.sources.twitter-source.channels = memory-channel
agent1.sinks.hdfs-sink.channel = memory-channel
```

##### 4. **Start Flume Agent**
```bash
flume-ng agent -n agent1 -f twitter.conf
```

##### 5. **Data Flow**
- Twitter API → Flume Source → Memory Channel → HDFS Sink

#### 🔹 **Use Case**
- Useful for **sentiment analysis**, **trending hashtags**, or **real-time dashboards**.


### Q3. Explain the architecture of Sqoop architecture and write a code about how to import and export a data using sqoop.

#### 🔹 **What is Sqoop?**
- Sqoop stands for **SQL-to-Hadoop**.
- Used to **import/export structured data** between **RDBMS and Hadoop**.

#### 🔹 **Sqoop Architecture**
- Sqoop runs as a **MapReduce job**.
- Utilizes **JDBC** to connect to RDBMS.
- Uses **mappers** to import/export data in parallel.
- Supports importing into **HDFS, Hive, or HBase**.

#### 🔹 **Import Flow**
1. User gives the import command.
2. Sqoop reads metadata from RDBMS.
3. Sqoop divides data into splits.
4. Mappers import chunks of data in parallel.
5. Data is saved in **HDFS** or **Hive**.


#### 🔹 **Export Flow**
1. User gives export command.
2. Sqoop reads data from HDFS.
3. Mappers push data into RDBMS.
4. Parallel insert/update operations.


#### 🔹 **Sample Commands**

##### ✅ **Import Data into HDFS**
```bash
sqoop import \
--connect jdbc:mysql://localhost:3306/company \
--username root \
--password root123 \
--table employees \
--target-dir /user/hadoop/employees \
--num-mappers 1
```

##### ✅ **Import Data into Hive**
```bash
sqoop import \
--connect jdbc:mysql://localhost:3306/company \
--username root \
--password root123 \
--table employees \
--hive-import \
--hive-table employees_hive \
--create-hive-table
```

##### ✅ **Export Data from HDFS to MySQL**
```bash
sqoop export \
--connect jdbc:mysql://localhost:3306/company \
--username root \
--password root123 \
--table employees \
--export-dir /user/hadoop/employees \
--input-fields-terminated-by ','
```

#### 🔹 **Use Case**
- Useful in **data warehousing**, **ETL workflows**, and **data lake creation**.

---
# **Unit 4: MongoDB, PyMongo, Spark & Spark SQL**

## 2 Marks
### **Q1. How Document is represented in MongoDB?**
- A document in MongoDB is a **JSON-like structure** called **BSON** (Binary JSON).
- Example:
  ```json
  {
    "_id": 1,
    "name": "Caine",
    "age": 30,
    "skills": ["Music", "Coding"]
  }
  ```
- It's schema-less and supports nested documents.


### **Q2. How to add a single data in MongoDB?**
- Use the `insertOne()` method.
- Example in Mongo shell:
  ```js
  db.users.insertOne({ name: "Caine", age: 30 });
  ```
- In PyMongo:
  ```python
  db.users.insert_one({"name": "Caine", "age": 30})
  ```


### **Q3. Define RDD in Spark**
- RDD = **Resilient Distributed Dataset**
- It is the **core abstraction** in Spark representing an immutable, distributed collection of objects.
- Supports **parallel operations**, **fault tolerance**, and **lazy evaluation**.


### **Q4. What are the functions of Spark SQL?**
- Allows querying structured data using SQL and DataFrame API.
- Functions:
  - `select()`, `filter()`, `groupBy()`, `join()`, `agg()`
  - Executes **SQL queries** using `spark.sql()`
- Supports integration with Hive and optimizations via Catalyst engine.


### **Q5. What is meant by lazy evaluation in Spark?**
- Transformations (like `map`, `filter`) are **not executed immediately**.
- Spark **waits until an action** (like `collect`, `count`) is called.
- Helps **optimize execution plans** and reduce unnecessary computations.


### **Q6. How do you set deploy mode in PySpark?**
- Use `--deploy-mode` option in the `spark-submit` command.
- Example:
  ```bash
  spark-submit --deploy-mode client app.py
  spark-submit --deploy-mode cluster app.py
  ```
- `client` runs driver on local machine; `cluster` runs driver on cluster node.

## 16 Marks
### Q1. Explain in detail about the Ecosystem of MongoDB with appropriate diagrams and explore collections and documents in MongoDB.

#### 🔹 **Overview of MongoDB Ecosystem**
MongoDB is a **NoSQL database** designed for handling large volumes of **unstructured data**. It has a rich ecosystem of tools, frameworks, and integrations to help with **data storage**, **processing**, and **analysis**.

##### Key Components of the MongoDB Ecosystem:
1. **MongoDB Database**: The core database that stores collections of documents.
2. **Collections**: Grouping of documents in MongoDB.
3. **Documents**: Individual records stored in collections.
4. **MongoDB Shell**: Interactive shell to interact with the database.
5. **MongoDB Drivers**: APIs in various programming languages (like Java, Python, Node.js) to connect and work with MongoDB.
6. **MongoDB Atlas**: A fully managed cloud database service for MongoDB.
7. **MongoDB Compass**: A GUI tool for visually exploring and interacting with your MongoDB data.
8. **Aggregation Framework**: Allows complex queries and data manipulation.
9. **Replication**: Ensures data availability and redundancy by duplicating data across multiple servers.
10. **Sharding**: Distributes data across multiple machines to ensure scalability.
11. **MongoDB Charts**: Visualization tool to create dashboards directly from MongoDB data.


#### 🔹 **Exploring Collections in MongoDB**
- **Collection**: A collection is a **group of MongoDB documents**. It is analogous to a **table in relational databases**.
- **Characteristics**:
  - Collections have **no fixed schema**.
  - Documents in a collection may have different fields and data types.
  - There is **no limit to the number of documents** in a collection.
- **Naming**:
  - A collection name must be a **string** and can contain lowercase and special characters, but cannot contain **null or spaces**.
  

#### 🔹 **Exploring Documents in MongoDB**
- **Document**: A document is a **data record** in MongoDB and is represented in **BSON (Binary JSON)** format.
- **Structure**:
  - A document is essentially a **JSON object**.
  - A document consists of **field-value pairs** where the field is a **key** and the value can be a variety of data types (string, integer, array, sub-document).
  - Every document has an implicit **_id** field that is a unique identifier (can be custom or autogenerated).
  
  Example Document:
  ```json
  {
    "_id": 1,
    "name": "Caine",
    "age": 30,
    "skills": ["Music", "Coding"],
    "address": {
      "street": "123 Main St",
      "city": "New York"
    }
  }
  ```

#### 🔹 **How Collections and Documents Work Together**
- A **collection** holds **documents**.
- **Documents** within the collection can have different structures (schemas) but generally share similar characteristics or data.
- MongoDB uses **indexes** to improve search performance in collections.


#### 🔹 **MongoDB Data Flow (Overview)**
1. **Data is inserted into collections**.
2. **Documents** are stored in **collections**, which can be queried, updated, and deleted.
3. **Aggregation** operations can be performed on documents within collections to analyze data.

---

#### 🔹 **Use Cases of MongoDB Ecosystem**
- **Content Management**: MongoDB is great for storing dynamic and unstructured content, like blogs, e-commerce product catalogs, etc.
- **Real-Time Analytics**: Used for big data applications where high-speed writes and flexible data models are needed.
- **IoT**: Handles large amounts of time-series or sensor data, where each document represents a reading or event.
- **Mobile & Web Apps**: Perfect for real-time updates and scalable apps with rapidly changing data models.

#### 🔹 **Diagram of MongoDB Ecosystem**
The **MongoDB ecosystem diagram** can look like this:

```
            +----------------------------+
            |       MongoDB Database     |
            +----------------------------+
                          |
            +-------------+--------------+
            |                            |
    +-------------------+      +-------------------+ 
    |   Collections     |      |      Tools &      |
    |   (Group Docs)    |      |    Integrations   |
    +-------------------+      +-------------------+
            |                          |
    +-------------------+      +-------------------+
    |    MongoDB Shell  |      |    MongoDB Atlas  |
    | (CLI Interaction) |      | (Cloud DB Service)|
    +-------------------+      +-------------------+
```
 
### Q2. What is meant by NoSQL? Explain in detail about CRUD operations in MongoDB.
#### **What is meant by NoSQL?**

- **NoSQL** stands for **Not Only SQL**, meaning it refers to **non-relational databases**.
- Unlike traditional **relational databases (RDBMS)**, which use structured data and tables with fixed schemas, **NoSQL** databases are designed to handle **unstructured, semi-structured, or structured data**.
- They are highly **scalable**, **flexible**, and support **varied data models** like key-value, document, graph, or column-family.

#### **Key Characteristics of NoSQL Databases**:
1. **Schema-less**: Data can be stored without predefined schemas. Each record (document) can have a different structure.
2. **Scalability**: NoSQL databases are designed to scale horizontally, which makes them efficient at handling large volumes of data.
3. **High Availability**: They ensure **high availability** with **replication** and **distributed architecture**.
4. **Flexible Data Models**: Can store data in various formats, including JSON, XML, or key-value pairs.
5. **Eventual Consistency**: Many NoSQL databases prioritize availability and partition tolerance over consistency (according to the CAP theorem).

#### **Types of NoSQL Databases**:
1. **Document Store**: Stores data as **documents** (e.g., MongoDB, CouchDB).
2. **Key-Value Store**: Stores data as key-value pairs (e.g., Redis, DynamoDB).
3. **Column-Family Store**: Organizes data into columns rather than rows (e.g., Cassandra, HBase).
4. **Graph Database**: Stores data in nodes, edges, and properties (e.g., Neo4j, Amazon Neptune).

#### ✅ **CRUD Operations in MongoDB**

CRUD stands for **Create**, **Read**, **Update**, and **Delete**. These operations are essential for interacting with MongoDB and are supported by its drivers, including MongoDB Shell and PyMongo.

##### **1. Create Operation** (`insertOne()`, `insertMany()`)
- **Purpose**: Insert new documents into a collection.
  
- **Example**:
  - Insert **a single document**:
    ```js
    db.users.insertOne({
      "name": "Caine",
      "age": 30,
      "skills": ["Music", "Coding"]
    });
    ```

  - Insert **multiple documents**:
    ```js
    db.users.insertMany([
      { "name": "Mevan", "age": 8, "skills": ["Art"] },
      { "name": "Zara", "age": 25, "skills": ["Design"] }
    ]);
    ```

##### **2. Read Operation** (`find()`, `findOne()`)
- **Purpose**: Retrieve documents from a collection.
  
- **Example**:
  - **Find all documents** in a collection:
    ```js
    db.users.find();
    ```

  - **Find specific documents** (filter by `age`):
    ```js
    db.users.find({ "age": { $gt: 20 } });
    ```

  - **Find a single document**:
    ```js
    db.users.findOne({ "name": "Caine" });
    ```

##### **3. Update Operation** (`updateOne()`, `updateMany()`, `replaceOne()`)
- **Purpose**: Modify existing documents in the collection.

- **Example**:
  - **Update one document**:
    ```js
    db.users.updateOne(
      { "name": "Caine" }, 
      { $set: { "age": 31 } }
    );
    ```

  - **Update multiple documents**:
    ```js
    db.users.updateMany(
      { "age": { $lt: 25 } },
      { $set: { "status": "young" } }
    );
    ```

  - **Replace a document**:
    ```js
    db.users.replaceOne(
      { "name": "Mevan" },
      { "name": "Mevan", "age": 9, "skills": ["Drawing"] }
    );
    ```


##### **4. Delete Operation** (`deleteOne()`, `deleteMany()`)
- **Purpose**: Remove documents from a collection.

- **Example**:
  - **Delete a single document**:
    ```js
    db.users.deleteOne({ "name": "Caine" });
    ```

  - **Delete multiple documents**:
    ```js
    db.users.deleteMany({ "age": { $lt: 20 } });
    ```


#### **Additional Notes on CRUD Operations**:
- MongoDB’s operations support **filters** and **operators** to specify conditions, such as `$gt`, `$lt`, `$eq`, `$ne`, etc.
- **Indexes** can be created for optimizing search performance during CRUD operations.
- **Atomicity**: Operations like `updateOne()` and `insertOne()` are atomic, meaning they are guaranteed to complete successfully, or not at all.

### Q3. Elaborate in detail about spark architecture with appropriate diagrams?

Apache Spark is a unified analytics engine for big data processing, with built-in modules for streaming, SQL, machine learning, and graph processing. Its architecture is designed to provide speed, ease of use, and the ability to handle a variety of data sources and formats. Below is a detailed explanation of the **Spark architecture** with its components and flow.

#### **Key Components of Spark Architecture**

1. **Driver Program**:
   - The **Driver** is the entry point for any Spark application. It manages the overall control and coordinates the work of **executors**.
   - It runs the **main()** function, responsible for creating the **SparkContext**, and coordinates the parallel execution of tasks.
   - The Driver interacts with the **Cluster Manager** to allocate resources and controls the **job scheduling**.

2. **Cluster Manager**:
   - **Cluster Manager** is responsible for managing resources in a cluster, including allocating and deallocating resources.
   - Spark supports various cluster managers like:
     - **Standalone**: Spark's own cluster manager.
     - **YARN (Yet Another Resource Negotiator)**: A resource manager for Hadoop ecosystems.
     - **Mesos**: A distributed systems kernel.
   - The **Cluster Manager** negotiates resources with the **Driver** and assigns tasks to **executors**.

3. **Executors**:
   - Executors are the **worker nodes** in a Spark cluster that run tasks assigned by the **Driver**.
   - Each executor runs in its own Java Virtual Machine (JVM), and multiple tasks can be run in parallel within the executor.
   - Executors are responsible for **storing data** in memory (using Spark's Resilient Distributed Datasets or RDDs) and **computing the results** of tasks.
   - They persist data and shuffle data between stages.
   - An executor exists for the entire lifetime of a Spark application.

4. **Worker Nodes**:
   - Worker nodes are the physical machines that run the **executors**.
   - These nodes are part of the cluster and communicate with the **Driver** to get tasks from the **Cluster Manager**.

5. **Resilient Distributed Datasets (RDDs)**:
   - RDDs are the fundamental data structure of Spark. They represent a **distributed collection of objects** that can be processed in parallel.
   - They are immutable and fault-tolerant, meaning they can handle failures by recomputing lost data from the lineage.
   - Operations on RDDs are either **narrow** (like `map()`, `filter()`) or **wide** (like `groupBy()`, `reduceByKey()`).

6. **Stages** and **Tasks**:
   - Spark divides work into **stages** based on **wide transformations** (those that require data shuffling, e.g., `groupBy()`, `reduceByKey()`).
   - Each stage is split into multiple **tasks**, which are distributed across the **executors**.
   - A task is the smallest unit of work and corresponds to one **partition** of the data.
   

#### **Execution Flow in Spark**

1. **Application Submission**:
   - The **user** submits a Spark application (through the `spark-submit` command).
   - The application contains the **Driver** program with tasks and transformations.

2. **Job Scheduling**:
   - The **Driver** requests the **Cluster Manager** for resources.
   - The **Cluster Manager** allocates resources and launches **executors**.
   - The **Driver** divides the application into jobs, and jobs into stages based on transformations.

3. **Task Execution**:
   - **Stages** are divided into **tasks**, each corresponding to a partition of the data.
   - Tasks are scheduled to be executed on **executors** by the **Driver**.

4. **Data Shuffling**:
   - In **wide transformations**, Spark performs **shuffling** to redistribute data across partitions.
   - Shuffling happens between **executors**, which can cause significant network overhead.

5. **Completion**:
   - Once all tasks are complete, the **executors** send the results back to the **Driver**.
   - The **Driver** completes the application, and the final output is displayed or saved to external storage.

---

#### **Diagram of Spark Architecture**:

Below is a diagram that illustrates the key components of the **Spark architecture**.

```
+-----------------------------------------------------+
|                     Driver Program                  |
| +----------------------+--------------------------+ |
| | SparkContext         | Job Scheduler            | |
| | (Coordinates jobs)   | (Manages task execution) | |
| +----------------------+--------------------------+ |
+--------------------------+--------------------------+
                           |
                           |
             +------------------------------+
             |       Cluster Manager        |
             |  (Allocates resources)       |
             +------------------------------+
                           |
   +-----------------------+-------------------------+
   |                       |                         |
+--------+            +--------+              +--------+
| Worker |            | Worker |              | Worker |
| Node   |            | Node   |              | Node   |
| (Execs)|            | (Execs)|              | (Execs)|
+--------+            +--------+              +--------+
       |                   |                       |
+------+--------+     +-----+--------+        +------+--------+
| Executor 1    |     | Executor 2   |        | Executor 3    |
| (Task Runner) |     | (Task Runner)|        | (Task Runner) |
+---------------+     +--------------+        +---------------+
       |                   |                       |
  +----+------+         +--+----------+         +--+----------+
  | Task 1    |         | Task 2      |         | Task 3      |
  | (RDD Part)|         | (RDD Part)  |         | (RDD Part)  |
  +-----------+         +-------------+         +-------------+
```

#### **Summary of Spark Architecture**:

- **Driver Program** controls the application.
- **Cluster Manager** allocates resources to the **executors**.
- **Executors** perform the **tasks** in parallel, process data, and store results.
- **RDDs** are the core data structure used for distributed data processing.
- **Stages** and **tasks** manage the data processing in parallel across the cluster.
  
With this architecture, Spark provides **fault tolerance**, **high availability**, and **parallel data processing**, making it suitable for big data workloads.



### Q4. Explain in detail about the steps for building spark ML pipeline.  
### Q5. Explain in detail about Hyper parameter training and AutoML in pyspark.



