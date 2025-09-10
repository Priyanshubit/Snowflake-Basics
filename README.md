# Snowflake-Basics

# ❄️⚡ Snowflake Data Pipeline with Snowpipe  

This project demonstrates how to build a **real-time data ingestion pipeline** using **Snowflake, AWS S3, and Snowpipe**.  
The pipeline automatically ingests **CSV files** from an external **S3 bucket** into a **Snowflake table** for seamless analytics.  

---

## 🎯 **Problem Statement**  
Manual data ingestion is **slow** ⏳ and **error-prone** ❌.  
➡️ To solve this, we use **Snowpipe** to **auto-load patient registration data** from AWS S3 → Snowflake, in **near real-time** ⏱️.  

---
## ⚙️ **Workflow Steps**

### 🔹 1. Database & Table Setup
```sql
USE DATABASE DATA_PIPELINE;

DROP TABLE IF EXISTS PIPELINE;

CREATE OR REPLACE TABLE PATIENTS(
  PATIENT_ID INTEGER PRIMARY KEY,
  FIRST_NAME VARCHAR(100),
  CITY VARCHAR(100),
  REGISTRATION INTEGER
);

SELECT * FROM PATIENTS;
```

### 🔹 2. Define CSV File Format
```sql
USE SCHEMA PUBLIC;

CREATE OR REPLACE FILE FORMAT my_csv_format
  TYPE = CSV
  FIELD_DELIMITER = ','
  SKIP_HEADER = 1
  NULL_IF = ('NULL', 'null');

SHOW FILE FORMATS IN SCHEMA PUBLIC;
```

### 🔹 3. Create External Stage (AWS S3)
```sql
CREATE OR REPLACE STAGE PATIENTS_AWS_STAGE
URL='S3://patients-data-snowpipe-pipeline'
CREDENTIALS=(
  AWS_KEY_ID='<your_aws_key>'
  AWS_SECRET_KEY='<your_aws_secret>'
)
FILE_FORMAT=MY_CSV_FORMAT;

SHOW STAGES;

```
💡 Stage = Connection between Snowflake & AWS S3 📂
