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
