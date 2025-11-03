# 📰 News Events Data Quality Pipeline

## 📘 Overview

This project automates the **data quality and preprocessing pipeline** for News Events data in JSONL format.
It ingests raw files, cleans and validates them, generates Data Quality (DQ) metrics, and uploads processed data into **Amazon Redshift** for analysis in BI tools like Tableau.

Built using **Streamlit** for interactivity and **AWS services** for backend orchestration, it ensures end-to-end automation, DQ governance, and alerting.

---

## ⚙️ Core Workflow

**1️⃣ Data Upload & Ingestion**

* Users upload JSONL files via the Streamlit UI.
* Files are stored in **Amazon S3 (raw bucket)** and parsed into:

  * `df_data`: Event details
  * `df_included`: Metadata (company, author, source)

**2️⃣ Preprocessing**

* Handles missing values and duplicates
* Cleans and standardizes date columns
* Detects outliers using the IQR method
* Removes long text fields incompatible with Redshift

**3️⃣ Data Profiling**

* Displays schema info, null counts, and unique values
* Generates category and confidence distributions
* Compares data before and after cleaning

**4️⃣ Redshift Integration**

* Automatically creates tables:

  * `news_events_data`
  * `news_events_included`
  * `dq_summary`
* Inserts cleaned data into Redshift
* Creates a BI-ready view `news_events_view`

**5️⃣ Data Quality & Alerts**

* Calculates DQ metrics: Completeness, Accuracy, Uniqueness, Consistency, Timeliness
* Stores metrics in Redshift
* Sends **SNS alerts** when DQ score < threshold

---

## ☁️ AWS Architecture

```
User Upload
    ↓
Amazon S3 (Raw Data)
    ↓
AWS Lambda (Validation & Transformation)
    ↓
Amazon Redshift (Tables & DQ Metrics)
    ↓
Streamlit Dashboard (EDA & Monitoring)
    ↓
AWS SNS (DQ Alerts)
```

---

## 📊 Key Outputs

* Cleaned CSVs:

  * `cleaned_df_data.csv`
  * `cleaned_df_included.csv`
* Redshift Tables:

  * `news_events_data`
  * `news_events_included`
  * `dq_summary`
* Alerts: Real-time SNS notifications

---

## 🧰 Tech Stack

**Frontend:** Streamlit
**Processing:** Pandas, NumPy, Matplotlib, Seaborn
**Cloud:** AWS S3, Redshift, Lambda, SNS, Secrets Manager
**Integration:** psycopg2, boto3

---

## 🚀 Benefits

* End-to-end automated DQ pipeline
* Real-time data validation & alerting
* Scalable and secure AWS integration
* Tableau-ready data for analytics

---

## 📁 Project Structure

```
news-data-quality-project/
│
├── app.py                        # Streamlit App
├── aws_lambda_trigger.py         # AWS Lambda trigger logic
├── redshift_sql_query.py         # Redshift schema setup
├── Datasets-2025-08-08/          # Sample datasets
├── News_Events_Data_Quality_Analysis_Pipeline.docx
├── Sample_Report.pdf
└── README.md                     # Project documentation
```

---
