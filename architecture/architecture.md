                 (Raw CSV files)
 Claims.csv   Customers.csv   Policies.csv   Handlers.csv
        \          |             |             /
         \         |             |            /
          v        v             v           v
      ┌───────────────────────────────────────────┐
      │        ADLS Gen2 / Delta Lake (Storage)    │
      └───────────────────────────────────────────┘
                          |
                          v
      ┌───────────────────────────────────────────┐
      │ BRONZE (Raw Delta Tables)                  │
      │ - Ingest raw files as Delta                │
      │ - Minimal changes (raw-by-design)          │
      └───────────────────────────────────────────┘
                          |
                          v
      ┌───────────────────────────────────────────┐
      │ SILVER (Clean + Validated + Enriched)      │
      │ - Drop missing PK + drop duplicates        │
      │ - Data quality checks + DQ flags           │
      │ - Impute missing values                    │
      │ - Derive features (duration, age, etc.)    │
      └───────────────────────────────────────────┘
                          |
                          v
      ┌───────────────────────────────────────────┐
      │ GOLD (Analytics-ready Star Schema)         │
      │ - FactClaim                                │
      │ - DimCustomer, DimPolicy, DimHandler,Date   │
      │ - OPTIMIZE + ZORDER (benchmarked)           │
      └───────────────────────────────────────────┘
                          |
                          v
      ┌───────────────────────────────────────────┐
      │ Power BI Report                             │
      │ - Page 1: Claim Overview                    │
      │ - Page 2: Manager & Efficiency              │
      └───────────────────────────────────────────┘
