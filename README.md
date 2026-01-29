# Local Data Lakehouse with Apache Iceberg

A high-performance local Data Lakehouse environment using Apache Iceberg, Spark Cluster, and Kafka Cluster. This is an enhanced fork optimized for modern data engineering standards.


## 🚀 Key Improvements
- **Clustered Setup**: Spark (1 Master, 2 Workers) and Kafka (3-node KRaft cluster).
- **Latest Stack**: Spark 3.5.5, Kafka 3.9.0, Trino 471, and Iceberg 1.10.0.
- **Modern Runtimes**: Powered by Java 17, Python 3.12, and PostgreSQL 16.
- **Native S3 Support**: Optimized S3 connectivity through Trino's native drivers and Hadoop 3.3.6.

## 🛠 Tech Stack
- **Apache Gravitino**: Iceberg REST Catalog management.
- **Apache Spark**: Distributed compute engine.
- **Apache Kafka**: Real-time message streaming.
- **Trino**: Fast distributed SQL query engine.
- **Prometheus & Grafana**: Observability and monitoring.
- **MinIO**: S3-compatible object storage (Data Lake).
- **Apache Iceberg**: High-performance table format.

## ⚡ Quick Start

1. **Launch Infrastructure**:
   ```shell
   docker compose up --detach --build
   ```

2. **Initialize Schema**:
   ```shell
   docker exec -it spark-master spark-sql -f /opt/spark/apps/setup/create_schema.sql
   ```

3. **Run a Pipeline**:
   ```shell
   docker exec -it spark-master python /opt/spark/apps/pipelines/create_example_table.py
   ```

4. **Using Notebooks**:
   - Access **JupyterLab** at `http://localhost:8888`.
   - Your notebooks are saved in the `notebooks/` directory.
   - To start a PySpark session in a notebook:
     ```python
     from pyspark.sql import SparkSession
     spark = SparkSession.builder.getOrCreate()
     ```

## 🔍 Querying Data
You can query tables using either Spark or Trino:

**Spark SQL:**
```shell
docker exec -it spark-master spark-sql
SELECT * FROM catalog_iceberg.schema_iceberg.table_iceberg;
```

**Trino CLI:**
```shell
docker exec -it trino trino --catalog catalog_iceberg --schema schema_iceberg
SELECT * FROM table_iceberg;
```

---
*Based on the original project by [marcellinus-witarsah](https://github.com/marcellinus-witarsah/local-data-lakehouse-iceberg).*
