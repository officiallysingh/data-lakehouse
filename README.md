# Data Lakehouse
**Comprehensive Guide following Medallion Architecture Pattern to implement Data Lakehouse Architecture**

## Introduction
The Data Lakehouse combines the flexibility, scalability, and cost-effectiveness of Data Lakes with the structured 
data management and governance features of Data Warehouses. 
The Medallion Architecture enhances this approach by logically segmenting data into layers i.e. Bronze, silver and Gold, providing clear separation, better management, and optimized access.

### Popular Lakehouse Solutions:
* Databricks Lakehouse Platform
* Snowflake Data Cloud
* AWS Lakehouse (S3 + Redshift Spectrum/Athena/Iceberg)
* Azure Synapse Analytics


## Features
1. **Unified Storage**: Storage platform or system capable of managing diverse types of data (structured, semi-structured, unstructured), 
enabling multiple workloads (batch processing, streaming, analytics, machine learning) on a common data repository.
2. **Open Data Formats**: Standardized, publicly available formats for storing and managing data. These formats prevent vendor lock-in, 
promote interoperability, enable seamless integration across tools and platforms, and facilitate schema evolution, governance, and efficient data processing.
3. **Transactional Support (ACID compliance)**: Ensures reliable and consistent data operations, 
allowing simultaneous read/write operations without conflicts or data corruption. It is crucial for maintaining data quality, integrity, and consistency
5. **Schema enforcement**: Ensures data conforms to predefined schemas, maintaining consistency and preventing corruption. 
6. **Schema evolution**: Allows schemas to adapt seamlessly as data and business requirements change, without requiring extensive reprocessing.
7. **Data Versioning**: Refers to maintaining multiple historical states of data, enabling recovery, auditing, and reproducing analytics.
8. **Time Travel**: Is the capability to query and analyze data as it existed at specific points in time.
9.**Data Governance**:
   * Metadata Management: Captures technical, operational, and business metadata (schema, owners, timestamps, lineage).
   * Data Cataloging: Organizes datasets into searchable inventories with metadata, schema, ownership, and usage stats.
   * Business Glossary: Maintains standardized business definitions for data elements (e.g., "Customer ID").
   * Data Classification: Tags data with sensitivity or domain labels (e.g., PII, financial, public).
   * Tagging: Attaches user-defined key-value annotations for search, ownership, or processing rules.
   * Data Lineage: Tracks the full journey of data: source → transformations → consumption (tables, reports, features).
   * Data Discovery: Enables users to search and explore data assets with metadata context and quality insights.
10. **Data Quality**: Ensures the data is accurate, on time, complete, consistent, conform to specified formats, ranges, constraints and trustworthy. 
   Poor data quality leads to incorrect insights, broken ML pipelines, regulatory non-compliance, and eroded trust among users.
11. **Data Security**: Since sensitive and business-critical data lives across layers, securing it requires multi-layered, fine-grained, and auditable controls.
    * Authentication: Verifying the identity of users, services, or applications.
    * Authorization (RBAC/ABAC): Defining what resources users can access and what operations they can perform.
    * Policy Management: Centralized management of security policies via governance tools.
    * Encryption: Protecting data at rest and in transit using encryption standards (AES-256, TLS).
    * Data Masking: Obfuscating or tokenizing sensitive data (e.g., PII, PHI).
    * Auditing & Monitoring: Tracking access and modifications to data and metadata.
12. **Data Sharing and Collaboration**: Share data across teams, departments, and even external partners in a secure and reliable manner.
13. **Advanced Analytics and AI/ML Integration**: Aggregations and joins on structured data, Experimentation using notebooks, BI tools integration.
14. **Query Performance Optimization**: Efficient query performance is crucial for a well-designed Data Lakehouse. 
As data volume and concurrency grow, optimizing performance across the storage, compute, query layers becomes essential.
15. **Observability**: Ensures transparency across the entire data pipeline—from ingestion to consumption—by capturing logs, metrics, and traces from processes such as Spark, NiFi, Airflow, etc.
It allows data engineers to monitor system health, performance, data quality, last updated timestamps for critical datasets.

## Medallion Architecture Overview
The Medallion Architecture is a design pattern for organizing data in Layers within a Data Lakehouse, popularized by platforms like Databricks. 
It provides clear guidance on managing data through different stages of maturity and refinement, promoting clarity, reliability, governance, and scalability.

1. **Bronze Layer 🥉(Raw Data)**
Acts as a foundational raw-data store, supporting historical retention, flexibility, and initial ingestion. 
Stores raw, unaltered data directly ingested from various sources. Minimal transformation occurs here.
* Data is stored in its original format (structured, semi-structured, or unstructured).
* Often uses schema-on-read, enabling flexible ingestion.
* Append-only to preserve historical ingestion records.
* Includes data lineage and ingestion metadata (timestamps, source identifiers, ingestion details).
* Example: Raw JSON logs from web servers or streaming data from Kafka topics are ingested and stored.

2. **Silver Layer 🥈 (Curated Data)**
Refine and cleanse data from Bronze Layer, making it consistent, structured, and queryable. The data in this layer is considered trusted and consumable for further processing, analytics and modeling.
* Cleansed, standardized, and validated data (schema enforcement, quality checks, deduplication).
* Data schema is explicitly defined (schema-on-write), evolved appropriately with versioning.
* Supports ACID transactions to ensure data reliability and consistency.
* Includes metadata for auditability, lineage, and data quality metrics.
* Example: Raw event logs (Bronze) are cleansed, parsed, and converted into structured tables with clear schemas for further processing.

3. **Gold Layer 🥇 (Aggregated & Business-ready Data)**
Provides aggregated, optimized, ready to serve data for business consumption i.e. analytics, reporting, dashboards, or AI/ML usage.
•	Highly refined and optimized datasets targeted for specific use cases.
•	Data is pre-aggregated or structured to support fast and efficient queries (e.g., fact tables, dimension tables, feature stores).
•	Optimized for performance through indexing, partitioning, Z-ordering, and caching.
•	Supports strict governance, security policies, and controlled access.
•	Example: Aggregated sales data by region, customer segments, monthly financial summaries, or precomputed ML feature tables ready for analytical tools or BI dashboards.

**Relation of Medallion Architecture to Data Lakehouse Features.**
It complements and leverages key Lakehouse features as follows.

| **Lakehouse Feature**                   | **Bronze**                 | **Silver**                                    | **Gold**                                |
|-----------------------------------------|----------------------------|-----------------------------------------------|-----------------------------------------|
| **Unified Storage & Open Formats**      | Raw storage                | Curated storage                               | Optimized storage                       |
| **Transactional (ACID Compliance)**     | Basic append-only          | Strong ACID compliance                        | Strong ACID compliance                  |
| **Schema Enforcement & Evolution**      | Schema-on-read             | Schema-on-write                               | Strict schema & optimization            |
| **Data Quality Management**             | Basic validations          | Extensive validation & cleansing              | High quality & audited data             |
| **Data Versioning & Time Travel**       | Basic retention            | Versioned & auditable                         | Strict data lineage and versioning      |
| **Metadata Management & Cataloging**    | Basic ingestion metadata   | Detailed metadata, lineage, cataloged schemas | Comprehensive business metadata         |
| **Data Governance & Security**          | Broad access               | Role-based, fine-grained controls             | Strict & fine-grained security policies |
| **Streaming & Batch Processing**        | Raw batch/stream ingestion | Curated streaming/batch processing            | Batch & streaming aggregations          |
| **Advanced Analytics & ML Integration** | NA                         | Refined data for further processing           | Optimized for ML/BI                     |
| **Query Performance Optimization**      | Minimal optimization       | Moderate optimization                         | Extensive optimization                  |


7.
8.	Data Security
9.	Data Quality Management
10.	Streaming & Batch Processing
11.	Scalability & Elasticity
12.	Separation of Storage & Compute
13.	Data Discovery & Cataloging

## Key Design Principles
* Scalability and elasticity
* Separation of storage and compute
* Schema evolution
* Data governance and lineage
* Data security and compliance
* Batch and real-time data ingestion, processing and serving

## Essential Features & Best Technologies

1. Storage Layer

Best Choice: MinIO
•	Alternatives: Apache HDFS, AWS S3, Google Cloud Storage

Criteria	MinIO	Apache HDFS	AWS S3
Scalability	High	Medium	High
Open Source	Yes	Yes	No (Managed)
Performance	High	Medium	High
Ease of Setup	Easy	Medium	Easy

2. Table Format

Best Choice: Apache Iceberg
•	Alternatives: Delta Lake, Apache Hudi

Criteria	Iceberg	Delta Lake	Hudi
Schema Evolution	Excellent	Good	Good
Performance	Excellent	Very Good	Good
Open Governance	Apache	Linux Found.	Apache
Compatibility	Spark, Flink	Spark, Flink	Spark, Flink

3. Compute Engine

Best Choice: Apache Spark
•	Alternatives: Apache Flink, PrestoDB, Trino

Criteria	Spark	Flink	PrestoDB/Trino
Batch Processing	Excellent	Good	Good
Real-time	Good	Excellent	Moderate
SQL Support	Strong	Moderate	Strong
Ecosystem	Extensive	Moderate	Good

4. Metadata Management & Data Governance

Best Choice: OpenMetadata
•	Alternatives: Apache Atlas, Marquez

Criteria	OpenMetadata	Apache Atlas	Marquez
Data Lineage	Excellent	Good	Excellent
Governance & Security	Excellent	Excellent	Moderate
Ease of Integration	Excellent	Moderate	Excellent
UI & User Experience	Excellent	Moderate	Good

5. Data Quality Management

Best Choice: Great Expectations
•	Alternatives: Deequ, Soda

Criteria	Great Expectations	Deequ	Soda
Community & Support	Excellent	Good	Good
Integration with Spark	Strong	Strong	Moderate
Flexibility	High	Medium	High

6. Feature Store (Real-Time Serving)

Best Choice: Feast with Cassandra (online store)
•	Alternatives: Hopsworks (managed/free tier), Tecton (paid)

Criteria	Feast/Cassandra	Hopsworks	Tecton
Real-time Serving	Excellent	Good	Excellent
Cost	Free	Free/Paid	Paid
Complexity	Medium	Medium	Low
Open Source	Yes	Partially	No

7. Data Ingestion

Best Choice: Apache NiFi (Real-Time) / Airflow (Batch)
•	Alternatives: Kafka Connect, AWS Glue

Criteria	NiFi	Airflow	Kafka Connect
Real-time Support	Excellent	Moderate	Excellent
Batch Jobs	Good	Excellent	Moderate
Ease of Use	Good	Excellent	Moderate
Integration	Extensive	Extensive	Moderate

Implementation Best Practices
•	Separate storage from compute to optimize costs.
•	Automate metadata capture for better lineage and governance.
•	Ensure security compliance via role-based access control (RBAC).
•	Regularly audit data quality and perform automated checks.
•	Maintain clear and structured documentation.

Conclusion

Implementing a Data Lakehouse with Medallion Architecture offers unparalleled scalability, robust governance, and streamlined analytics. By selecting the best open-source tools—such as Apache Iceberg, Spark, OpenMetadata, and MinIO—you ensure flexibility, cost efficiency, and enterprise-grade capabilities. Evaluate alternatives based on your specific use case and criteria to make informed technology choices that align with your organization’s objectives.

## References
- [Spring boot starter for Spark](https://github.com/officiallysingh/spring-boot-starter-spark).
- [Apache Hadoop and Hive installation guide](https://medium.com/@officiallysingh/install-apache-hadoop-and-hive-on-mac-m3-7933e509da90) for details on how to install Hadoop and Hive.
- To know about Spark Refer to [**Spark Documentation**](https://spark.apache.org/docs/latest/).
- Find all Spark Configurations details at [**Spark Configuration Documentation**](https://spark.apache.org/docs/latest/configuration.html)
- [Apache Iceberg](https://iceberg.apache.org/docs/nightly/)
- [Apache Iceberg Spark Quickstart](https://iceberg.apache.org/docs/1.9.0/java-api-quickstart/)
- [Apache Hadoop](https://hadoop.apache.org/)
- [Apache Hive](https://hive.apache.org/)
- [Nessie](https://projectnessie.org/iceberg/iceberg/)
