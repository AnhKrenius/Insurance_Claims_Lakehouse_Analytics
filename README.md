# Insurance Claims Analytics Platform
**End-to-End Lakehouse Analytics Project (Azure Databricks · Delta Lake · Power BI)**

This project demonstrates a **production-style data engineering and analytics workflow**, covering data ingestion, validation, transformation, optimization, and business reporting using a **Medallion (Bronze / Silver / Gold) Lakehouse architecture**.

The focus of the project is not only dashboarding, but **building a reliable, performant, and analytics-ready data foundation** that supports downstream BI use cases.

---

## 🎯 Project Objectives

- Design a scalable **Lakehouse architecture** suitable for real-world insurance analytics
- Implement robust **data quality checks, enrichment, and traceability**
- Build **fact and dimension models** optimized for BI consumption
- Apply **Delta Lake performance optimizations** and measure their impact
- Deliver management-focused **Power BI dashboards** on top of curated Gold tables

---

## 🏗️ Architecture Overview

**Core Technologies**
- **Azure Data Lake Gen2** – cloud storage for Bronze, Silver, and Gold layers
- **Azure Databricks (Spark)** – distributed processing and Delta Lake management
- **Delta Lake** – ACID transactions, schema enforcement, versioning
- **Power BI** – analytics and executive reporting
- **Git** – version control and reproducibility

**Architecture Pattern**
```
Raw Files → Bronze (Raw Delta)
→ Silver (Cleaned, Validated, Enriched)
→ Gold (Fact & Dimension Tables, Optimized)
→ Power BI Dashboards
```

---

## 🔄 Data Pipeline Breakdown

### 🟫 Bronze Layer — Raw Ingestion
- Ingested raw CSV datasets (Claims, Customers, Policies, Handlers)
- Stored as **Delta tables** in ADLS to enable:
  - Schema evolution
  - Time travel
  - Auditability
- No business logic applied at this stage (raw-by-design)

---

### 🟪 Silver Layer — Data Engineering Core (Key Strength)

The **Silver layer is the heart of this project** and where most data engineering work happens.

Implemented transformations include:

#### ✅ Data Quality & Validation
- Dropped records with missing primary keys
- Removed duplicate records based on business keys
- Validated date logic (e.g. create date ≤ close date)
- Detected invalid numerical values (negative claim amounts, outliers)

#### 🚩 Data Quality Flags (Not Hard Deletes)
Instead of blindly dropping data, **data quality issues are explicitly flagged**, enabling:
- Transparency
- Auditability
- Downstream decision-making

Example flags:
- `IsInvalidClaimDate`
- `IsNegativeClaimAmount`
- `IsOutlierClaimAmount`
- `IsMissingCustomer`
- `IsMissingPolicy`

This mirrors **real enterprise data engineering practices**.

#### 🧠 Enrichment & Feature Engineering
- Derived metrics:
  - Claim duration (days)
  - Customer age
  - Policy tenure
- Standardized categorical fields
- Prepared analytical features for BI and future ML use cases

---

### 🟨 Gold Layer — Analytics-Ready Modeling

The Gold layer exposes **business-ready datasets** optimized for analytics.

#### ⭐ Star Schema Design
- **FactClaim**
- **DimCustomer**
- **DimPolicy**
- **DimHandler**
- **DimDate**

Benefits:
- Simplified BI modeling
- Faster query performance
- Clear separation of facts and dimensions

#### 🧾 Table Registration
Gold Delta tables are **registered in Databricks metastore**, enabling:
- SQL access
- BI tool connectivity
- Centralized schema governance

---

## ⚡ Performance Optimization & Benchmarking

Gold tables were optimized using **Delta Lake best practices**:

### Optimization Techniques
- `OPTIMIZE` for file compaction
- `ZORDER BY (CustomerID, PolicyNumber)` for data skipping
- Metadata cleanup via `VACUUM`

### Measured Results (FactClaim Table)
| Query Type | Performance Improvement |
|----------|--------------------------|
| Read Queries | **61% faster** |
| Filter Queries | **74% faster** |
| Aggregations | **64% faster** |

Performance was **measured before and after optimization** using Databricks benchmarking notebooks.

These improvements translated into:
- Faster Power BI dataset refresh
- More responsive interactive filtering
- Reduced query latency

---

## 📊 Power BI Dashboards

Power BI dashboards were built directly on curated Gold tables and focus on **operational and management insights**, not raw reporting.

### Key Analytics Areas
- **Claims SLA compliance**
  - Assignment within 3 days
  - Closure within 30 days
- **Claim resolution duration**
- **Incident type & multi-vehicle claim analysis**
- **Handler and reporting manager efficiency**
- **Customer segmentation (Platinum focus)**
- **Geographic distribution of customers and claims**

### Dashboard Screenshots

#### Claims Overview
![Claims Overview](powerbi/screenshots/claim_overview.png)

#### Manager & Efficiency
![Manager Efficiency](powerbi/screenshots/manager_efficiency.png)

---

## 📁 Repository Structure

```
insurance-claims-analytics/
├── README.md
├── notebooks/
│ ├── 01_bronze_ingestion.ipynb
│ ├── 02_silver_transformation.ipynb
│ ├── 03_gold_modeling.ipynb
│ ├── 04_register_gold_tables.ipynb
│ └── 05_optimize_and_benchmark_factclaim.ipynb
├── powerbi/
│ ├── screenshots/
│ └── dashboard_description.md
├── docs/
│ ├── data_model.md
│ ├── kpi_definitions.md
│ └── performance_benchmark.md
└── architecture/
```


---

## 🔁 Reproducibility & Engineering Practices

- Modular notebooks with clear execution order
- Explicit separation of Bronze / Silver / Gold logic
- Version-controlled code and documentation
- Metrics-driven performance validation
- Architecture and KPI documentation included

---

## 📌 Notes

Cloud resources used for development are no longer active.  
This repository preserves the **full engineering design, transformation logic, performance benchmarks, and BI outputs** for portfolio and demonstration purposes.

---

## 👤 Target Roles

This project is suitable for:
- Data Engineer
- Analytics Engineer
- BI Engineer
- Senior Data Analyst (with engineering focus)

