# 🚀 End-to-End Data Engineering Project | Medallion Architecture | Airflow + DBT + Databricks + AWS

## 📌 Project Overview

This project demonstrates a complete **End-to-End Data Engineering Pipeline** using modern cloud and data engineering technologies.

The pipeline follows the **Medallion Architecture (Bronze → Silver → Gold)** and covers real-world enterprise data engineering scenarios including:

- Incremental Data Ingestion
- Metadata Driven Pipelines
- Data Quality Checks
- Schema Evolution
- Slowly Changing Dimensions (SCD)
- Dimensional Data Modeling
- Star Schema Design
- One Big Table (OBT) Creation
- Data Transformation using DBT
- Workflow Orchestration using Apache Airflow
- Cloud Data Lake Implementation using AWS S3
- Analytics-ready Data Warehouse using Databricks

The project simulates a production-grade data platform where raw data is ingested from multiple sources, transformed, validated, modeled, and prepared for business analytics.

---

# 🏗️ Architecture Overview

![Data Engineering Architecture](architecture.png)

The project follows the **Medallion Lakehouse Architecture**:

```
                Data Sources
                     |
        -----------------------------
        |                           |
   SQL Database                 AWS S3
        |                           |
        -------- Data Ingestion -----
                     |
              Apache Airflow
              (Orchestration)
                     |
              Databricks Lakehouse
                     |
        -----------------------------
        |            |              |
     Bronze       Silver          Gold
      Layer       Layer           Layer
        |            |              |
   Raw Data     Clean Data     Analytics
                 Models        Data Models
                     |
                  BI Tools
```

---

# 🛠️ Tech Stack Used

## Data Ingestion
- Apache Airflow
- SQL Agent
- AWS S3
- Python

## Data Processing & Transformation
- Databricks
- Apache Spark
- DBT (Data Build Tool)
- PySpark

## Cloud Platform
- AWS S3
- Databricks Lakehouse

## Data Modeling
- Star Schema
- Dimension Tables
- Fact Tables
- One Big Table (OBT)

## Orchestration
- Apache Airflow DAGs

## Data Architecture
- Medallion Architecture

---

# 🔄 Data Pipeline Workflow

## 1. Data Ingestion Layer

Data is ingested from multiple sources:

### Source Systems

### SQL Database
- Transactional data extracted using SQL jobs
- Incremental ingestion implemented using watermark columns

Example:

```
source_table
      |
      |
 incremental extraction
      |
      ↓
Databricks Bronze Layer
```


### AWS S3

Files are ingested from AWS S3:

```
AWS S3
 |
 |
Raw Files
 |
 |
Databricks Bronze
```

Supported scenarios:

- CSV ingestion
- JSON ingestion
- Incremental file processing
- Metadata-based ingestion

---

# 🥉 Bronze Layer (Raw Data Layer)

The Bronze layer stores raw ingested data without major transformations.

Responsibilities:

- Store historical raw data
- Maintain source data structure
- Preserve original data
- Enable reprocessing


Example:

```
bronze_customer
bronze_orders
bronze_products
```

Features:

✅ Raw ingestion  
✅ Schema tracking  
✅ Incremental loading  
✅ Metadata management  

---

# 🥈 Silver Layer (Cleaned & Transformed Layer)

DBT is used for transformation and data quality processing.

Transformations include:

### Data Cleaning

- Removing duplicate records
- Handling NULL values
- Standardizing formats
- Data type corrections


Example:

Before:

|customer_id|name|email|
|-|-|-|
|101|John|NULL|


After:

|customer_id|name|email|
|-|-|-|
|101|John|unknown@email.com|


---

## Schema Evolution

The pipeline handles schema changes dynamically.

Examples:

- New columns added
- Column datatype changes
- Source structure changes


Implemented using:

- Databricks Delta Lake
- DBT incremental models


---

# Data Quality Checks

DBT tests are implemented for:

### Unique Checks

Example:

```
customer_id should be unique
```


### Not Null Checks

Example:

```
customer_name cannot be NULL
```


### Referential Integrity

Example:

```
orders.customer_id 
must exist in customer table
```


---

# 🥇 Gold Layer (Analytics Layer)

The Gold layer contains business-ready datasets.

Implemented using:

- DBT Models
- Dimensional Modeling
- Star Schema


---

# ⭐ Star Schema Design


## Dimension Tables


### dim_customer

```
customer_key
customer_id
customer_name
customer_location
customer_segment
```


### dim_product

```
product_key
product_id
product_name
category
price
```


---

## Fact Tables


### fact_sales

```
sales_key
customer_key
product_key
order_date
quantity
sales_amount
```


---

# Slowly Changing Dimensions (SCD)

Implemented SCD Type 2 to maintain historical changes.

Example:


Customer Address Change:

Before:

```
Customer 101
Address = New York
Active = True
```


After:

```
Customer 101
Address = New York
Active = False


Customer 101
Address = California
Active = True
```


Maintains complete historical tracking.

---

# One Big Table (OBT)

Created analytical datasets by combining:

- Fact tables
- Dimension tables


Example:

```
sales_obt

customer information
+
product information
+
sales metrics
+
date information
```


Used for:

- BI dashboards
- Reporting
- Machine Learning features

---

# 🔄 Apache Airflow Orchestration

Airflow manages the complete workflow.


Pipeline DAG:


```
Start

 |
 |
Extract Data
 |
 |
Load Bronze Layer
 |
 |
DBT Transformation
 |
 |
Data Quality Checks
 |
 |
Create Silver Models
 |
 |
Create Gold Models
 |
 |
End

```


Airflow handles:

✅ Scheduling  
✅ Dependency management  
✅ Pipeline monitoring  
✅ Failure handling  
✅ Job retries  


---

# 📂 Project Structure

```
Data-Engineering-Project
│
├── airflow
│   ├── dags
│   │   └── pipeline_dag.py
│
├── dbt_project
│   │
│   ├── models
│   │   |
│   │   ├── bronze
│   │   ├── silver
│   │   └── gold
│   │
│   ├── tests
│   ├── snapshots
│   └── dbt_project.yml
│
├── databricks
│   ├── notebooks
│   └── jobs
│
├── scripts
│
├── configs
│
├── requirements.txt
│
└── README.md
```

---

# 🚀 Pipeline Execution Flow


## Step 1: Ingest Data

Sources:

```
SQL Server
AWS S3
```

↓

## Step 2: Store Raw Data

```
Databricks Bronze Layer
```

↓

## Step 3: Execute DBT Models

Transform:

```
Bronze
 |
 |
Silver
 |
 |
Gold
```

↓

## Step 4: Run Data Quality Checks

DBT Tests:

```
dbt test
```

↓

## Step 5: Generate Analytics Tables

Create:

- Fact Tables
- Dimension Tables
- OBT Tables


---

# 📊 Analytics Use Cases

The final datasets support:

- Sales Analytics
- Customer Analytics
- Product Performance Analysis
- Business Reporting
- Dashboard Development
- Machine Learning Feature Engineering


---

# 🔐 Data Engineering Best Practices Implemented

✔ Medallion Architecture  
✔ Incremental Processing  
✔ Metadata Driven Framework  
✔ Data Validation  
✔ Schema Evolution  
✔ Modular DBT Models  
✔ SCD Type 2  
✔ Dimensional Modeling  
✔ Automated Pipeline Scheduling  
✔ Cloud Data Lake Architecture  


---

# 📈 Future Enhancements

- Add CI/CD using GitHub Actions
- Deploy Airflow using Docker/Kubernetes
- Add Data Observability using Great Expectations
- Add Streaming Pipeline using Kafka
- Implement Terraform Infrastructure Automation


---

# 👨‍💻 Author

**Vinod Paritala**

Data Engineer | Cloud Data Engineer | Big Data Enthusiast

Skills:

- Azure Data Engineering
- AWS
- Databricks
- Apache Spark
- DBT
- Apache Airflow
- SQL
- Python


---

⭐ If you like this project, consider giving it a star!
