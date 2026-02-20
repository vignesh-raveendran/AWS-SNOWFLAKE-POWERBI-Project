# 🌾 Agricultural Intelligence Platform  
### End-to-End Cloud Analytics & Business Intelligence

![AWS](https://img.shields.io/badge/AWS-S3_%26_IAM-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![Snowflake](https://img.shields.io/badge/Snowflake-Data_Warehouse-29B5E8?style=for-the-badge&logo=snowflake&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-Data_Visualization-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![SQL](https://img.shields.io/badge/SQL-ELT_Pipelines-4479A1?style=for-the-badge&logo=mysql&logoColor=white)

---

# 📌 Executive Overview

This project demonstrates a modern cloud data architecture designed to process, transform, and visualize **15 years of agricultural data (3,158 records)** across major districts in Karnataka, India.

By leveraging a decoupled cloud stack:

- **AWS S3** → Data Lake Storage  
- **Snowflake** → Cloud Data Warehouse & ELT Processing  
- **Microsoft Power BI** → Business Intelligence & Dashboarding  

Raw environmental and agronomic flat files were transformed into a highly interactive **4-page BI dashboard suite**, enabling stakeholders to analyze complex correlations between climate conditions and crop yields.

---

# 🏗️ System Architecture

```
AWS S3 (Raw CSV Data)
        │
        ▼
Snowflake Storage Integration (IAM Role)
        │
        ▼
External Stage
        │
        ▼
Snowflake Data Warehouse
        │
        ▼
ELT Transformations (Feature Engineering)
        │
        ▼
Power BI Semantic Model
        │
        ▼
4-Page Dashboard Suite
```
---

# 🎯 Business Objective

Enable agricultural planners and agribusiness stakeholders to:

- Analyze relationships between rainfall, temperature, humidity, and yield
- Identify optimal growing seasons
- Detect environmental anomalies
- Support risk-informed crop planning decisions

---

# ⭐ STAR Method Analytical Framework

## 🟡 Situation

Historical agricultural datasets containing crop yields, soil details, and granular weather parameters were confined to static CSV files (`data_season.csv`).  

The absence of a centralized, scalable data warehouse limited multidimensional analysis and prevented advanced agronomic forecasting.

---

## 🟢 Task

Design and implement a scalable cloud-native ELT pipeline to:

- Securely store raw agricultural data  
- Build a structured cloud data warehouse  
- Engineer analytical features  
- Develop a 4-page interactive BI dashboard categorized into:
  - Yield Analytics
  - Rainfall Analysis
  - Temperature Impact
  - Humidity Trends

---

## 🔵 Action

- Provisioned AWS S3 data lake (`power-bi.project`)
- Configured AWS IAM role (`powerbi.role`) with strict trust policies
- Created Snowflake Storage Integration for credential-less access
- Engineered ELT workflows using Snowflake SQL
- Created non-destructive replica tables for safe transformation
- Engineered new analytical features:
  - `year_group`
  - `rainfall_groups`
- Simulated environmental constraints (e.g., rainfall intensification, area reduction)
- Imported transformed dataset into Power BI using Import Mode (VertiPaq engine)
- Designed intuitive 4-page semantic BI dashboard suite

---

## 🟣 Result

Delivered a fully automated cloud analytics platform that:

- Identified **Rabi season’s superior yield efficiency**
- Flagged environmental anomalies for governance
- Enabled seasonal and climatic yield comparison
- Provided executive-ready agricultural intelligence dashboards

---

# ⚙️ Cloud Engineering & Snowflake Implementation

## 1️⃣ Security Integration & Infrastructure

```sql
CREATE OR REPLACE STORAGE INTEGRATION powerbi_integration
TYPE = EXTERNAL_STAGE
STORAGE_PROVIDER = 'S3'
ENABLED = TRUE
STORAGE_AWS_ROLE_ARN = 'arn:aws:iam::<account-id>:role/powerbi.role'
STORAGE_ALLOWED_LOCATIONS = ('s3://power-bi.project/');
```

---

## 2️⃣ External Stage Creation

```sql
CREATE STAGE agriculture_stage
URL = 's3://power-bi.project/'
STORAGE_INTEGRATION = powerbi_integration;
```

---

## 3️⃣ Bulk Data Ingestion

```sql
COPY INTO agriculture_dataset
FROM @agriculture_stage
FILE_FORMAT = (TYPE = CSV FIELD_DELIMITER = ',' SKIP_HEADER = 1)
ON_ERROR = 'CONTINUE';
```

---

# 🔄 ELT & Feature Engineering

To preserve raw data integrity:

```sql
CREATE TABLE agriculture_analysis AS
SELECT * FROM agriculture_dataset;
```

---

## 📊 Engineered Features

### Year Group Categorization

```sql
UPDATE agriculture_analysis
SET year_group =
    CASE
        WHEN year BETWEEN 2005 AND 2010 THEN '2005-2010'
        WHEN year BETWEEN 2011 AND 2015 THEN '2011-2015'
        ELSE '2016-2020'
    END;
```

---

### Rainfall Binning

```sql
UPDATE agriculture_analysis
SET rainfall_groups =
    CASE
        WHEN rainfall < 500 THEN 'Low Rainfall'
        WHEN rainfall BETWEEN 500 AND 1000 THEN 'Moderate Rainfall'
        ELSE 'High Rainfall'
    END;
```

---

# 📊 Power BI Dashboard Suite

### 1️⃣ Yield Intelligence
- Crop yield by season
- District-wise yield comparison
- Seasonal performance benchmarking

<img width="1312" height="723" alt="Screenshot 2026-02-20 125717" src="https://github.com/user-attachments/assets/4511ffd4-f2cc-497f-a664-6de5a6bb9034" />


### 2️⃣ Rainfall Analysis
- Rainfall vs Yield correlation
- Rainfall distribution by district
- Rainfall group performance impact

<img width="1316" height="728" alt="Screenshot 2026-02-20 125757" src="https://github.com/user-attachments/assets/69945c65-ef18-4250-82e4-8cd7957864d5" />


### 3️⃣ Temperature Impact
- Temperature fluctuations across years
- Yield sensitivity to heat variation

<img width="1311" height="722" alt="Screenshot 2026-02-20 125742" src="https://github.com/user-attachments/assets/d1cdd4fd-7f71-4bb3-bbf3-d1354f85607f" />


### 4️⃣ Humidity Trends
- Humidity vs productivity insights
- Seasonal moisture volatility tracking

<img width="1312" height="728" alt="Screenshot 2026-02-20 125730" src="https://github.com/user-attachments/assets/72bfae47-c05d-4f93-b3a2-8d677f5006c4" />


---

# 📈 Key Performance Indicators (KPIs)

- Total Crop Yield (Metric Tons)
- Average Rainfall (mm)
- Seasonal Yield Efficiency Ratio
- District Productivity Ranking
- Rainfall Group Performance Index
- Environmental Anomaly Detection Rate

---

# 💡 Key Insights

- Rabi season demonstrates higher yield efficiency compared to Kharif.
- Moderate rainfall range yields optimal crop productivity.
- Extreme rainfall variability correlates with yield instability.
- Temperature spikes negatively impact seasonal output consistency.

---

# 🧠 Skills Demonstrated

### ☁️ Cloud Engineering
- AWS S3 Data Lake Provisioning
- IAM Trust Policy Configuration
- Secure Snowflake Integration

### 🏢 Data Warehousing
- Snowflake External Stages
- COPY INTO ingestion workflows
- ELT architecture design

### 🧮 Advanced SQL
- Feature engineering
- Categorical binning
- Non-destructive transformation modeling

### 📊 Business Intelligence
- Power BI semantic modeling
- VertiPaq optimization
- Multi-page executive dashboard design

---

# 🚀 Business Impact

✔ Enables data-driven agricultural planning  
✔ Improves seasonal risk management  
✔ Identifies climate-driven productivity shifts  
✔ Supports agribusiness operational strategy  
✔ Demonstrates scalable modern cloud analytics architecture  

---

# 📷 Dashboard Preview

![WEATHERYIELDANALYSISUSINGAWSANDSNOWFLAKE-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/029bc3c9-549a-4858-80ba-5353885cf3f0)

---

# 🔮 Future Enhancements

- Integrate real-time weather APIs
- Implement predictive yield forecasting (Machine Learning)
- Automate ingestion using Snowflake Tasks & Streams
- Add district-level soil health modeling
- Deploy role-based Power BI access control

---

## ✍️ Author

**Vignesh Raveendran**  
*Data Engineer / Data Analyst*  

[LinkedIn](https://www.linkedin.com/in/yourprofile) | [Portfolio](https://yourportfolio.com)
