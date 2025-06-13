# **VII Kafka**

#### **Q1. Explain in detail about Kafka data streaming with its components and architecture.**

**Apache Kafka** is a **distributed streaming platform** used for building real-time data pipelines and streaming apps.

---

### ✅ **Key Components:**

1. **Producer**

   * Sends (publishes) data to Kafka topics.

2. **Consumer**

   * Subscribes to topics and processes incoming data.

3. **Broker**

   * Kafka server that stores messages. A cluster can have multiple brokers.

4. **Topic**

   * Logical channel where data is published (like a queue).

5. **Partition**

   * Topic is split into partitions for parallel processing and scalability.

6. **Zookeeper** *(in older versions)*

   * Manages cluster metadata and leader election.

7. **Consumer Group**

   * Set of consumers sharing a topic's partitions (used for load balancing).

---

### 🧠 **Kafka Architecture Overview:**

```
             +----------------+
             |    Producer    |
             +--------+-------+
                      |
                      v
                +-----------+
                |  Kafka    |  (Cluster of Brokers)
                |  Broker   |
                +-----------+
                |  Topics   |
                | Partitions|
                +-----------+
                      |
                      v
              +----------------+
              |    Consumer    |
              +----------------+
```

---

### ⚙️ **How Streaming Works:**

1. Producers **send messages** to Kafka topics.
2. Kafka **stores messages** in partitions (order preserved within each).
3. Consumers **pull messages** from topics in real-time.
4. Offset-based reading allows fault tolerance and replay.

---

### 📌 **Use Cases:**

* Log aggregation
* Real-time analytics
* Event sourcing
* Streaming ETL
* Monitoring & alerting systems

---

### ✅ **Exam Tip Summary:**

* Kafka = real-time, distributed, durable
* Key terms: Producer, Consumer, Topic, Partition, Broker
* Architecture: Message flows from producer → broker → topic → partition → consumer
