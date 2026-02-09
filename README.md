# DataMigrationToAzure-ADF -- My First Project

## 📌 Project Overview

This project demonstrates building a complete **End-to-End Data Engineering pipeline on Microsoft Azure** using **Azure Data Factory (ADF)**.

The pipeline automates:

- Ingestion of external data files
- Processing and transformation of data
- Storage of optimized data in Azure Data Lake
- Execution automation
- Version control integration using GitHub

The project simulates real-world enterprise data ingestion workflows.

---

##  Architecture
![image_alt](https://github.com/omaga333/DataMigrationToAzure-ADF/blob/05282771eb68e148ae0197abbb019ef63be286e5/Diagram.jpg)
---


## 🎯 Project Objectives

The main goals of the project:

- Automate ingestion of multiple files
- Transform raw data into structured format
- Handle schema variations
- Store optimized analytics-ready data
- Create reusable pipelines
- Integrate pipelines with Git version control

---


---

## ⚙️ Technologies Used

- Azure Data Factory (ADF)
- Mapping Data Flow
- Integration Runtime
- Azure Data Lake Storage
- Parquet file format
- Snappy compression
- GitHub integration

---

## 🔄 Pipeline Workflow

### Step 1: File Discovery
Files are collected dynamically from source systems.

Sources include:
- SFTP servers
- Local systems
- On-prem sources

![imaga_alt](https://github.com/omaga333/DataMigrationToAzure-ADF/blob/057cf51a72dee32d272ee0e97c2a183932ad668b/pipeline/Apiingest.png)


![imaga_alt](https://github.com/omaga333/DataMigrationToAzure-ADF/blob/057cf51a72dee32d272ee0e97c2a183932ad668b/pipeline/Incremental%20Load.png)

![imaga_alt](https://github.com/omaga333/DataMigrationToAzure-ADF/blob/057cf51a72dee32d272ee0e97c2a183932ad668b/pipeline/onpremingest.png)

---

### Step 2: ForEach Activity
Pipeline loops through files automatically.

Purpose:
- Process multiple files
- Avoid manual pipeline execution

---

### Step 3: Copy Activity
Raw data is copied to Azure Storage staging area.

Functions:
- Secure transfer
- Prepare for transformation

---

### Step 4: Mapping Data Flow Transformation
Transformation operations include:

- Schema mapping
- Data cleaning
- Type conversion
- Column selection
- Data formatting

  ![imaga_alt](https://github.com/omaga333/DataMigrationToAzure-ADF/blob/057cf51a72dee32d272ee0e97c2a183932ad668b/pipeline/silver.png)

Executed using Spark clusters managed by ADF.

---

### Step 5: Optimized Output Storage
Processed data stored as:

- Parquet files
- Snappy compression

Benefits:
- Faster analytics
- Reduced storage size
- Efficient Spark processing

---

## 🧠 Parameterization Strategy

Parameters were used to:

- Pass file paths dynamically
- Handle variable file names
- Reuse pipelines for multiple datasets

Result:
Reusable and scalable pipelines.
![imaga_alt](https://github.com/omaga333/DataMigrationToAzure-ADF/blob/4c56cf26216fde64b2169c2576cd013f8ddd8ffa/pipeline/Dynamic%20Mapping.png)
---

## 🔁 Alter Row Transformation Usage

Alter Row transformation controls database operations.

Example configuration:

Upsert if: 1 > 0

Meaning:
All rows are treated as Upsert operations.

Used during development to simplify testing.

Production logic typically uses key matching:


---

## 🧮 Ranking Functions Learning

### RANK()

Ranks values but skips numbers after ties.

Example:

| Score | Rank |
|------|------|
| 100  | 1 |
| 100  | 1 |
| 90   | 3 |

---

### DENSE_RANK()

Ranks values without skipping numbers.

Example:

| Score | Dense Rank |
|------|-------------|
| 100  | 1 |
| 100  | 1 |
| 90   | 2 |


![imaga_alt](https://github.com/omaga333/DataMigrationToAzure-ADF/blob/50803c8c138909d438a906b048c2fad2b41aaeb5/pipeline/rank.png)

---

### Usage Difference
- Use **RANK** when gaps are acceptable.
- Use **DENSE_RANK** when ranking must remain continuous.

---

## ⚠️ Issues Encountered & Fixes

### Issue: ForEach received String instead of Array
Error:foreach expression is of type 'String'
Fix:
Converted input to array.

---


## 📈 Skills Demonstrated

This project demonstrates:

- ETL pipeline design
- Data ingestion automation
- Schema management
- Transformation pipelines
- Parameterized pipelines
- Debugging Spark jobs
- Azure service integration
- Git-based version control


## In the Gold Layer, we created business-ready views to provide curated data for reporting and analytics. Below is an example of one such business view.

![imaga_alt](https://github.com/omaga333/DataMigrationToAzure-ADF/blob/62af4ba567d608ff009b0d6703df116aab268389/pipeline/gold.png)
![imaga_alt](https://github.com/omaga333/DataMigrationToAzure-ADF/blob/62af4ba567d608ff009b0d6703df116aab268389/pipeline/GoldView.png)





## ⏱ Pipeline Scheduling using ADF Triggers

To automate pipeline execution, Azure Data Factory Triggers were configured.

### Trigger Usage

Triggers were created to automatically execute pipelines without manual intervention.

Types used include:

- Scheduled triggers for periodic execution
- Parameterized execution for dynamic runs

---


## 🔔 Monitoring & Alerting using Azure Logic Apps

To ensure pipeline reliability, automated alerting was implemented using Azure Logic Apps.

---
![imaga_alt](https://github.com/omaga333/DataMigrationToAzure-ADF/blob/262a5cfad05c86f1ffceea4fac46949106402eda/pipeline/Alert.png)

## 🔔 Monitoring & Alerting using Azure Logic Apps

Pipeline failure or execution events flow **horizontally**:

**Pipeline Failure or Execution Event → Azure Monitor Event Trigger → Logic App Execution → Email / Notification Alert**


### Implementation Details

- Pipeline execution events are monitored.
- Azure Monitor triggers Logic App workflows.
- Notifications are sent automatically upon failures.

### Benefits

- Immediate failure detection
- Faster troubleshooting
- Production-ready monitoring setup
- Reduced manual monitoring

---

### Real Scenario Example

If a Spark Data Flow job fails:

1. Failure event is detected.
2. Logic App workflow runs automatically.
3. Alert notification is sent.
4. Pipeline issue can be investigated quickly.

---
## 🔗 GitHub / Azure DevOps Integration

![imaga_alt](https://github.com/omaga333/DataMigrationToAzure-ADF/blob/3b9368c9843e80aa3b15513c3e2d9582bbbc38da/pipeline/AzureDevops.png)


To ensure proper version control and collaboration, the ADF project was integrated with **GitHub**.

### Purpose
- Maintain a versioned copy of the project
- Enable rollback to previous versions
- Support teamwork and collaboration

### Implementation Details
1. **Import Existing Resources**  
   - Existing pipelines, datasets, and data flows were imported into the repository.
2. **Branch Creation**  
   - Main branch (`main`) was used for development.
   - Publish branch (`adf_publish`) stores deployment-ready versions.
3. **Publish & Commit**  
   - All changes in ADF were committed to Git.
   - Publishing from ADF ensures the latest pipeline is available in the repository.

### Benefits
- Full project history and version control
- Ability to collaborate with multiple developers
- Safeguards against accidental loss of work
- Supports CI/CD workflows in future improvements







