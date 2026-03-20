# ADF Medallion Architecture Pipeline — Azure Data Engineering Project

![ADF](https://img.shields.io/badge/Azure%20Data%20Factory-0089D6?style=flat&logo=microsoft-azure&logoColor=white)
![DataLake](https://img.shields.io/badge/Azure%20Data%20Lake-0078D4?style=flat&logo=microsoft-azure&logoColor=white)
![Status](https://img.shields.io/badge/Pipeline%20Status-Succeeded-brightgreen)

## Overview

An end-to-end cloud data pipeline built on Azure implementing the
Medallion Architecture (Bronze → Silver → Gold) for airline booking data.
The pipeline ingests data from three sources — on-premises SQL, REST API,
and incremental SQL loads — orchestrates them via a parent pipeline,
and applies multi-layer transformations using ADF Dataflows and Mapping
Data Flows before serving analytics-ready Gold layer outputs.

---

## Architecture

![ADF Medallion Architecture](https://github.com/user-attachments/assets/529dade8-bdab-484e-b718-9478609dd18b)

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Azure Data Factory | Pipeline orchestration and dataflows |
| Azure Data Lake Gen2 | Layered storage (Bronze / Silver / Gold) |
| ADF Mapping Data Flows | Visual transformations and aggregations |
| Self-Hosted Integration Runtime | On-premises SQL data ingestion |
| REST API Integration | API source ingestion |
| Azure Logic Apps | Email failure alerting |
| GitHub | Version control via ADF Git integration |

---

## Data Model

Built on an airline booking domain with a star schema:

| Table | Type | Description |
|---|---|---|
| FactBooking | Fact | Core booking transactions |
| DimAirline | Dimension | Airline reference data |
| DimFlight | Dimension | Flight details |
| DimPassenger | Dimension | Passenger profiles |
| DimAirport | Dimension | Airport reference data |

---

## Pipeline Layers

### Bronze — Raw Ingestion
Three child pipelines run sequentially under a parent orchestrator:
- `ExecuteOnPrem` — ingests raw data from on-premises SQL via SHIR
- `ExecuteAPI` — ingests data from REST API source
- `ExecuteIncremental` — incremental load from SQL to Data Lake

### Silver — Transformation Layer
ADF Dataflow applies transformations per dimension and fact table:
- Column derivation (gender flags, name formatting, airport enrichment)
- Data type casting on FactBooking ticket costs
- Row filtering (age > 25 for passenger dimension)
- AlterRow policies for upsert logic on all 5 streams

### Gold — Serving Layer
ADF Dataflow joins FactBooking with DimAirline, applies:
- Left outer join on booking and airline keys
- Column selection and aggregation (TotalSales per airline)
- Window function for revenue ranking
- Top-N filter to surface highest performing airlines

---

## Pipeline Screenshots

### Silver Layer — Data Transformation Dataflow
<img width="1918" height="763" alt="image" src="https://github.com/user-attachments/assets/70cbbc45-ca27-4ca6-b299-b0c924353594" />

### Gold Layer — Serving and Aggregation Dataflow
<img width="1920" height="770" alt="image" src="https://github.com/user-attachments/assets/fac60aaf-ec65-4559-a54c-e0c2e2af8646" />

### Parent Pipeline — Orchestration with Successful Run
<img width="1887" height="827" alt="image" src="https://github.com/user-attachments/assets/b9aa2733-d13d-498b-a0c5-b46c4c57eab2" />

### Failure Alert — Logic App Email Notification
<img width="1022" height="687" alt="image" src="https://github.com/user-attachments/assets/2c6827cc-c0b8-476a-a733-039bda329349" />


---

## Pipeline Run Evidence

| Activity | Status | Duration |
|---|---|---|
| ExecuteOnPrem | Succeeded | 33s |
| ExecuteAPI | Succeeded | 22s |
| ExecuteIncremental | Succeeded | 56s |
| FailureAlert | Succeeded | 6s |

---

## Key Engineering Decisions

- Used parent-child pipeline pattern to separate ingestion concerns
  and enable independent re-runs of each source
- Implemented Logic App webhook for failure alerting instead of
  ADF-native email to demonstrate cross-service integration
- Applied window ranking in Gold layer to avoid hardcoded top-N
  filtering — makes the pipeline reusable for any date range
- Used AlterRow transformation with upsert policy to make Silver
  layer idempotent — safe to re-run without duplicates

---

## Project Structure
```
ADF-Medallion-Project/
│
├── pipeline/          # ADF pipeline JSON definitions
├── dataflow/          # Mapping Data Flow definitions
├── dataset/           # Dataset definitions
├── linkedService/     # Linked service configurations
├── integrationRuntime/# SHIR configuration
└── factory/           # ADF factory settings
```

---

## How to Deploy

1. Fork this repository
2. In Azure Data Factory, go to Manage → Git configuration
3. Connect to your forked GitHub repo
4. ADF will automatically import all pipelines, dataflows and datasets
5. Update linked services with your own connection strings
6. Publish and trigger the ParentPipeline

---

*Built by Manish Patil — Final Year IT Engineering Student, SPPU, Pune*
*Connect on [LinkedIn]https://www.linkedin.com/in/manish-patil-009389321*
