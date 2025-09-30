# 🚀 Azure Data Factory - Medallion Architecture Project

## 📘 Overview
This project demonstrates an **end-to-end Data Pipeline** using **Azure Data Factory (ADF)**, integrating data from **SQL**, **API**, and **On-Prem** sources into **Azure Data Lake** following the **Medallion Architecture (Bronze, Silver, Gold)**.

The goal is to automate data movement, transformation, and curation using **ADF activities and triggers**.

---

## ⚙️ Tools & Technologies
- **Azure Data Factory (ADF)**
- **Azure Data Lake**
- **SQL Database**
- **REST API Integration**
- **Self-Hosted Integration Runtime (SHIR)**
- **GitHub** (Version Control)

---

## 🧱 Architecture
Below is the high-level architecture of the project:

![ADF Medallion Architecture]
<img width="1344" height="768" alt="adf-project-arch" src="https://github.com/user-attachments/assets/529dade8-bdab-484e-b718-9478609dd18b" />


### 🥉 Bronze → 🥈 Silver → 🥇 Gold Layers
- **Bronze:** Raw data ingestion  
- **Silver:** Cleaned and structured data  
- **Gold:** Analytics-ready curated data  

---

## 🔄 Pipeline Flow
1. Extract data from SQL, API, and On-Prem sources  
2. Load raw data into **Bronze layer**  
3. Apply transformations and cleansing to **Silver layer**  
4. Aggregate and prepare curated data for **Gold layer**  
5. Automate execution using **ADF triggers**

---

## 🧰 Key Learnings
- Building **ADF pipelines** with multiple sources  
- Setting up and using **SHIR**  
- Implementing **Medallion Architecture**  
- Managing **datasets, linked services, and triggers**  
- Understanding **end-to-end data orchestration**

---

## 📈 Outcome
This project helped me gain **hands-on experience** with Azure Data Factory, data lake layering, and pipeline automation — key skills in **Azure Data Engineering**.

---

## 👤 Author
**Manish Patil**  
💼 Data Engineer | Azure | ADF | Data Lake | SQL | API Integration  
🔗 [GitHub Profile]([https://github.com/your-username](https://github.com/patilmanish1486))

