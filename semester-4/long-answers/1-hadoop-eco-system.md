# **Hadoop Ecosystem**

#### **Q1. Distributed File System, Big Data Characteristics & Scalability Dimensions**

**Distributed File System**:

* Stores data across multiple nodes.
* Ensures fault tolerance and parallel access.
* Example: HDFS in Hadoop.

**Characteristics of Big Data (5 V’s):**

1. **Volume** – Large size of data
2. **Velocity** – Speed of data generation
3. **Variety** – Structured, semi-structured, unstructured
4. **Veracity** – Uncertainty and noise in data
5. **Value** – Insights gained from analysis

**Dimensions of Scalability:**

* **Storage scalability** – Add more nodes for more capacity
* **Compute scalability** – Handle larger workloads by adding compute nodes
* **Performance scalability** – Maintain efficiency with scale

---

#### **Q2. File Read and File Write in Hadoop**

**File Write Process:**

1. Client contacts NameNode to request write.
2. File is split into blocks (default 128 MB).
3. Data is written to DataNodes in a pipeline (with replication).
4. Acknowledgements are sent back to the client.

**File Read Process:**

1. Client asks NameNode for block locations.
2. Client reads blocks directly from respective DataNodes.
3. Combines and presents to the application.

**Diagram Tip**: Show NameNode, DataNodes, block splitting, replication.

---

#### **Q3(i). Compare Hadoop with Traditional Systems**

| Feature         | Hadoop                    | Traditional Systems            |
| --------------- | ------------------------- | ------------------------------ |
| Storage         | Distributed (HDFS)        | Centralized or local           |
| Processing      | Parallel using MapReduce  | Sequential                     |
| Scalability     | Horizontal (add nodes)    | Limited vertical scaling       |
| Fault Tolerance | High (data replication)   | Low (single point of failure)  |
| Cost            | Open-source, low cost     | Expensive enterprise solutions |
| Data Types      | Structured + unstructured | Mostly structured              |

---

#### **Q3(ii). Six Hadoop Commands**

1. **`hdfs dfs -ls /path`** – Lists files in HDFS directory
2. **`hdfs dfs -put localfile /hdfs/path`** – Uploads file to HDFS
3. **`hdfs dfs -get /hdfs/path localfile`** – Downloads file from HDFS
4. **`hdfs dfs -mkdir /path`** – Creates a new directory in HDFS
5. **`hdfs dfs -rm /path/file`** – Deletes a file from HDFS
6. **`hdfs dfsadmin -report`** – Shows cluster summary

---

#### **Q4. Main Hadoop Components & MapReduce**

**Main Components:**

* **HDFS** – Storage layer
* **MapReduce** – Processing engine
* **YARN** – Resource manager
* **Common Utilities** – Shared libraries and tools

**MapReduce Concepts:**

* **Map** – Processes input into key-value pairs
* **Shuffle & Sort** – Groups similar keys
* **Reduce** – Aggregates results

**Diagram Tip**: Show flow: Input → Map → Shuffle → Reduce → Output

---

#### **Q5. Hadoop 2.0 Architecture**

**Key Features:**

* Introduced **YARN**: Splits Resource Management and Job Scheduling
* Supports multiple processing models (e.g., Spark, Tez)
* Improved scalability and fault tolerance
* High availability with Standby NameNode

**Architecture Components:**

* **ResourceManager (YARN)** – Manages cluster resources
* **NodeManager** – Manages each node’s tasks
* **ApplicationMaster** – Manages the life cycle of each application

**Diagram Tip**: Show Client → ResourceManager → NodeManagers with containers
