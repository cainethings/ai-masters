# **Unit 3: Data Ingestion (Sqoop & Flume)**

## 2 Marks
### 1) Compare sqoop and flume
- **Sqoop** is used for importing/exporting data between **RDBMS and Hadoop**.
- **Flume** is used for **real-time ingestion** of streaming/log data into Hadoop.
- Sqoop works best for **structured, batch-based data**.
- Flume is ideal for **event-driven, unstructured or semi-structured data**.
- Sqoop connects to **databases**; Flume connects to **data sources like logs, Twitter, etc.**

### 2) How can we control the number of mappers using sqoop?
- Use the option `--num-mappers` or shorthand `-m` in the Sqoop command.   
- Default is **4 mappers**.   
- To control parallelism or reduce load, set it manually (e.g., `--num-mappers 1`).  
- Useful when importing small tables or when splitting is not feasible.
- **Example:** ```sqoop import --connect jdbc:mysql://localhost/db --table employees --num-mappers 2```

## 16 Marks
### 1) Explain in detail about data ingestion tools available in big data and how the data’s are ingested into the model.

#### 🔹 **What is Data Ingestion?**
- It is the process of collecting and transferring data from various sources to a storage or processing system.
- Sources include databases, logs, sensors, social media, cloud, APIs, etc.
- Can be **batch-based** or **real-time (streaming)**.

---

#### 🔹 **Types of Data Ingestion**
- **Batch Ingestion** – Large volumes of data moved at intervals (e.g., daily, hourly).
- **Real-Time Ingestion** – Data is ingested continuously as it is generated.

---

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

---

#### 🔹 **How Data Is Ingested into Big Data Models**

- **Step 1: Connect to Data Sources**
  - Tools like Sqoop connect to **databases**, Flume to **log/event sources**, and Kafka to **message producers**.

- **Step 2: Ingest Data into Hadoop Ecosystem**
  - Data is pushed into **HDFS**, **Hive**, or **HBase** for storage.

- **Step 3: Processing with Tools**
  - Tools like **Spark**, **MapReduce**, or **HiveQL** process the ingested data.

- **Step 4: Load into Models**
  - Cleaned and processed data is used to **train machine learning models** or for **data analysis**.

---

#### 🔹 **Example Use Case (Elaboration)**

> Suppose an e-commerce website wants to analyze customer behavior:
- **Flume** collects real-time clickstream data from web servers.
- **Sqoop** imports customer profile data from MySQL into Hive.
- Data is processed using **Spark SQL**.
- Final dataset is used to build a **recommendation model**.


2. Elaborate in detail about the steps for extracting twitter data using flume.  
3. Explain the architecture of Sqoop architecture and write a code about how to import and export a data using sqoop.

---

# **Unit 4: MongoDB, PyMongo, Spark & Spark SQL**

## 2 Marks
1. How Document is represented in MongoDB?  
2. How to add a single data in MongoDB?  
3. Define RDD in spark.  
4. What are the functions of Spark SQL?  
5. What is meant by lazy evaluation in Spark?  
6. How do you set deploy mode in Pyspark?

## 16 Marks
1. Explain in detail about the Ecosystem of MongoDB with appropriate diagrams and explore collections and documents in MongoDB.  
2. What is meant by NoSQL? Explain in detail about CRUD operations in MongoDB.  
3. Elaborate in detail about spark architecture with appropriate diagrams?  
4. Explain in detail about the steps for building spark ML pipeline.  
5. Explain in detail about Hyper parameter training and AutoML in pyspark.



