# Big Data Placement Notes

This document is a **comprehensive Big Data revision guide** for placement preparation. It combines theory, commands, quick tables, and Q&A.

---

## 1. Big Data Fundamentals

### What is Big Data?

- Extremely large datasets that cannot be processed by traditional computing techniques
- Requires specialized tools and technologies for storage, processing, and analysis
- Generated from various sources like social media, sensors, transactions, etc.

### Characteristics (5 V's)

| V | Meaning | Example |
|---|---------|---------|
| Volume | Huge data size | Petabytes of logs |
| Velocity | Speed of generation | Stock market ticks |
| Variety | Different formats | Text, images, JSON |
| Veracity | Trustworthiness | Fake reviews, typos |
| Value | Extracted insights | Fraud detection |

---

## 2. Hadoop Ecosystem

### HDFS Architecture

- **NameNode**: Metadata, namespace
- **DataNode**: Stores actual blocks (default 128MB)
- **Replication**: Default 3 copies
- **Secondary NameNode**: Merges logs with FSImage

### MapReduce Workflow

1. Input Split → 2. Map → 3. Shuffle & Sort → 4. Reduce → 5. Output

### YARN Architecture

- **ResourceManager**: Global scheduler
- **NodeManager**: Per-node manager
- **ApplicationMaster**: Per-job resource negotiator
- **Container**: Unit of CPU + Memory

---

## 3. Comparison Tables

### Traditional vs Big Data

| Feature | Traditional | Big Data |
|---------|-------------|----------|
| Storage | RDBMS | HDFS |
| Processing | Single machine | Cluster computing |
| Schema | Schema-on-write | Schema-on-read |
| Scalability | Vertical | Horizontal |
| Cost | Expensive | Commodity hardware |

### Hive vs HBase vs HDFS

| Feature | Hive | HBase | HDFS |
|---------|------|-------|------|
| Type | Data Warehouse | NoSQL DB | File Storage |
| Use Case | Analytics | Real-time updates | Store raw data |
| Schema | Schema-on-write | Dynamic columns | None |

### MapReduce vs Spark

| Feature | MapReduce | Spark |
|---------|-----------|-------|
| Speed | Disk-based, slow | In-memory, fast |
| API | Java | Scala, Python, R, SQL |
| Use Cases | Batch | Batch + Streaming + ML |
| Fault Tolerance | Replication | Lineage (RDD) |

---

## 4. Key Tools

- **Hive** → SQL-like queries on HDFS
- **Pig** → Dataflow scripts → Converts to MR jobs
- **Sqoop** → Import/export between RDBMS & HDFS
- **Flume** → Ingest streaming data into HDFS/HBase
- **HBase** → Column-family NoSQL DB
- **Kafka** → Distributed messaging system
- **Spark** → In-memory cluster computing (batch + streaming + ML)

---

## 5. Architectures

### Lambda vs Kappa

- **Lambda** = Batch + Speed + Serving layer
- **Kappa** = Only streaming, replay events

### Kafka Workflow

- **Producer → Broker → Topic (Partitions) → Consumer Groups**

### Spark Architecture

- **Driver → Cluster Manager → Executors → Tasks**

---

## 6. Command Cheat Sheet

```bash
# HDFS Commands
hadoop fs -ls /user
hadoop fs -put file.txt /user/hdfs/
hadoop fs -cat /user/hdfs/output.txt

# Run MapReduce Job
hadoop jar wordcount.jar input/ output/

# Spark Submit
spark-submit --class org.example.WordCount wc.jar input.txt output

# Sqoop Import
sqoop import --connect jdbc:mysql://localhost/db --table ORDERS --username user --password pass
```

---

## 7. Q&A

**Q: Why block size = 128MB?**
A: To reduce costly seek time, ensure transfer >> seek time.

**Q: Combiner vs Reducer?**
A: Combiner runs on Mapper node (mini-reducer) to reduce network traffic.

**Q: Hive vs HBase?**
A: Hive for analytics, HBase for real-time updates.

**Q: Spark Fault Tolerance?**
A: Achieved using lineage info of RDDs.

**Q: PageRank in MR?**
A: Iterative algorithm using matrix-vector multiplication, probabilistic surfer model.

---

## 8. Real-World Applications

- **Fraud detection** → Real-time Spark + Kafka
- **Recommendation systems** → Hadoop + MLlib
- **IoT sensor data** → HBase + Flume + Spark Streaming
- **Social media analytics** → Hive + Spark SQL
- **Healthcare** → Predictive analytics with TensorFlow on Spark

---