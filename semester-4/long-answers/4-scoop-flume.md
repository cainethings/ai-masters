
# **IV Data Ingestion Tools (Sqoop, Flume)**

---

#### **Q1. Explain in detail about data ingestion tools available in big data and how the data’s are ingested into the model.**

**Data Ingestion** is the process of collecting and loading data from multiple sources into Big Data systems.

**Types of Ingestion:**

* **Batch ingestion** – Data is loaded at scheduled intervals (e.g., Sqoop).
* **Real-time ingestion** – Data is streamed continuously (e.g., Flume, Kafka).

**Popular Tools:**

1. **Sqoop** – Transfers data between RDBMS (like MySQL) and Hadoop (HDFS/Hive).
2. **Flume** – Collects log/streaming data (e.g., from Twitter, web servers).
3. **Kafka** – High-throughput real-time messaging system.
4. **Nifi** – GUI-based tool to automate data flows.

**Usage in Model Building:**

* Ingested data is stored in **HDFS**, **Hive**, or **NoSQL**.
* Processed using **Spark/Hive**.
* Finally fed into **ML models** or dashboards.

---

#### **Q2. Elaborate in detail about the steps for extracting Twitter data using Flume.**

**Steps to Extract Twitter Data using Flume:**

1. **Install Flume.**

2. **Get Twitter Developer Access:**

   * Create app at [Twitter Developer Portal](https://developer.twitter.com).
   * Get: `Consumer Key`, `Consumer Secret`, `Access Token`, `Access Token Secret`.

3. **Configure Flume agent (`twitter.conf`):**

```properties
agent.sources = twitterSource
agent.sinks = hdfsSink
agent.channels = memoryChannel

agent.sources.twitterSource.type = org.apache.flume.source.twitter.TwitterSource
agent.sources.twitterSource.consumerKey = <YourKey>
agent.sources.twitterSource.consumerSecret = <YourSecret>
agent.sources.twitterSource.accessToken = <YourToken>
agent.sources.twitterSource.accessTokenSecret = <YourTokenSecret>
agent.sources.twitterSource.keywords = bigdata,hadoop

agent.sinks.hdfsSink.type = hdfs
agent.sinks.hdfsSink.hdfs.path = hdfs://localhost:9000/twitter_data/

agent.channels.memoryChannel.type = memory

agent.sources.twitterSource.channels = memoryChannel
agent.sinks.hdfsSink.channel = memoryChannel
```

4. **Run Flume agent:**

```bash
flume-ng agent --conf conf --conf-file twitter.conf --name agent -Dflume.root.logger=INFO,console
```

---

#### **Q3. Explain the architecture of Sqoop and write a code about how to import and export data using Sqoop.**

**Sqoop Architecture:**

* **Connectors:** Interface between Sqoop and RDBMS (e.g., MySQL).
* **Sqoop Client:** CLI to submit commands.
* **MapReduce Jobs:** Sqoop internally uses MapReduce to parallelize import/export.
* **HDFS/Hive/HBase:** Target systems to load/export data.

**Sqoop Import Command:**

```bash
sqoop import \
--connect jdbc:mysql://localhost/employees \
--username root \
--password root \
--table emp \
--target-dir /user/emp_data \
--m 1
```

**Sqoop Export Command:**

```bash
sqoop export \
--connect jdbc:mysql://localhost/employees \
--username root \
--password root \
--table emp_backup \
--export-dir /user/emp_data \
--m 1
```

---

**Exam Summary:**

* **Sqoop** = RDBMS ↔ Hadoop (Batch)
* **Flume** = Streaming logs/Twitter → HDFS (Real-time)
* Mention one import/export command for each, and highlight source/target clearly.
