
### **1. Hadoop Ecosystem**

**Q: What is meant by distributed file system?**
>A system that stores data across multiple machines, providing fault tolerance and scalability.

**Q: List out the file formats supported by HDFS.**
>Text, Sequence, Avro, Parquet, ORC, and RCFile.

**Q: What are the significant features in Hadoop 2.0?**
>YARN for resource management, high availability, and support for non-MapReduce frameworks.

**Q: How name-node failure is handled in Hadoop ecosystem?**
>By using a standby NameNode for high availability and automatic failover.

**Q: What is the difference between external table and managed table?**
>In managed tables, Hive controls data; in external tables, data remains outside Hive.

---

### **2. Hive**

**Q: Define metastore in Hive.**
>It’s a central repository that stores metadata about Hive tables and partitions.

---

### **3. Sqoop and Flume**

**Q: Compare Sqoop and Flume.**
>Sqoop is for importing/exporting data between RDBMS and Hadoop; Flume is for streaming log data into Hadoop.

**Q: How can we control the number of mappers using Sqoop?**
>By using the `--num-mappers` option in the command.

---

### **4. Kafka**

**Q: Name the important components of Kafka.**
>Producer, Consumer, Broker, Topic, and Zookeeper.

**Q: How is a Kafka Server started?**
>By running the `kafka-server-start.sh` script with a server configuration file.

---

### **5. MongoDB**

**Q: How Document is represented in MongoDB?**
>As a JSON-like structure called BSON (Binary JSON).

**Q: How to add a single data in MongoDB?**
>Use `db.collection.insertOne({key: "value"})`.

---

### **6. Spark**

**Q: Define RDD in Spark.**
>Resilient Distributed Dataset – a fault-tolerant collection of elements for parallel processing.

**Q: What are the functions of Spark SQL?**
>It enables querying structured data using SQL or DataFrame APIs.

**Q: What is meant by lazy evaluation in Spark?**
>Execution is delayed until the result is needed, improving performance.

**Q: What are the different data types supported by Spark MLlib?**
>Vectors, LabeledPoint, Matrices, and basic types like Double and Int.

**Q: How do you set deploy mode in Pyspark?**
>Using `--deploy-mode` in `spark-submit` (e.g., `client` or `cluster`).

---

### **7. General Big Data Concepts**

**Q: List out any five real time applications of big data.**
>Fraud detection, Recommendation engines, Healthcare analytics, Customer insights, and Traffic management.

**Q: What are the 5 V’s involved in big data ecosystem?**
>Volume, Velocity, Variety, Veracity, and Value.

**Q: Define AutoML.**
>Automated Machine Learning that simplifies model building and selection without manual tuning.

---
