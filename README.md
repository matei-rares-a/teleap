# Enterprise Portfolio Project: **Connected Vehicle Telemetry Analytics Platform**

Given AUMOVIO's focus on mobility, sensors, and software-defined vehicles, an **automotive telemetry data platform** is the ideal theme — it directly mirrors the domain and hits every skill in the job description.

---

## Project Concept

Build an end-to-end data platform that ingests simulated vehicle sensor data (speed, braking events, battery status, GPS coordinates), transforms it through a medallion architecture (bronze → silver → gold), stores it in a data warehouse, and surfaces it through interactive Power BI dashboards for "fleet managers" and "quality engineers."

This is enterprise-grade because it involves **multiple data sources, layered transformations, role-based access, scheduling, and business-facing reporting** — not just a single notebook.

---

## Recommended Stack (mapped to the JD)

| JD Requirement | What You'll Use |
|---|---|
| ETL/ELT pipelines | **Python** (pandas, PySpark) + **Databricks** (Community Edition — free) |
| Data warehouse | **Databricks Lakehouse** or **AWS Redshift** (free tier) |
| Database modeling | **Star schema** — fact tables (telemetry events, braking events) + dimension tables (vehicles, drivers, locations, time) |
| SQL | All warehouse queries + transformations in **SQL** |
| Power BI | **Power BI Desktop** (free) with **DAX** measures and **Power Query M** for staging |
| Git | Full repo on **GitHub** with branching, PRs, and README |
| Automation (bonus) | **GitHub Actions** or **Jenkins** for pipeline scheduling |
| Cloud (bonus) | **AWS Free Tier** (S3 for raw landing zone, Redshift for warehouse) or **Azure** (Blob Storage + Synapse) |
| Data Science (basic) | One predictive model — e.g., anomaly detection on braking patterns using scikit-learn |

---

## Architecture to Build

```
[Data Sources]          [Ingestion]         [Warehouse]           [Serving]
                                                
Simulated CSV/JSON  →  Python ETL scripts  →  Bronze (raw)       
  - sensor readings     scheduled via         Silver (cleaned)   →  Power BI
  - braking events      GitHub Actions/        Gold (aggregated)     Dashboards
  - GPS traces          Airflow/cron            ↑                     
  - weather API                            Star Schema Design        
                                           (fact + dimensions)       
```

---

## Concrete Deliverables (what interviewers will see)

1. **GitHub Repo** with clean structure:
   - `/pipelines` — Python ETL scripts (ingestion, cleaning, aggregation)
   - `/sql` — DDL for star schema, transformation queries
   - `/models` — simple anomaly detection notebook
   - `/dashboards` — Power BI `.pbix` file + screenshots
   - `/infra` — Docker Compose or Terraform for reproducibility
   - `README.md` — architecture diagram, setup instructions, design decisions

2. **Data Model Documentation** — an ERD showing your star schema with fact_telemetry, fact_braking_events, dim_vehicle, dim_driver, dim_location, dim_time

3. **Power BI Dashboard** (3–4 pages):
   - Fleet overview (KPIs, map visual, filters by vehicle/region)
   - Braking analysis (trends, anomaly flags, drill-through)
   - Quality metrics (defect rates by component, time series)
   - Use **DAX** for calculated measures (rolling averages, YoY comparisons) and **Row-Level Security (RLS)** to demonstrate data permission management

4. **Pipeline orchestration** — even a simple cron/GitHub Actions schedule that runs daily shows you understand production workflows

---

## Data Sources (all free)

| Source | What It Gives You |
|---|---|
| [Kaggle — Vehicle Telemetry Dataset](https://www.kaggle.com/datasets) | Search "vehicle telemetry", "OBD-II", or "fleet data" |
| [OpenWeatherMap API](https://openweathermap.org/api) | Weather context to join with driving data (free tier) |
| Python `faker` + custom scripts | Generate realistic sensor readings at scale (100K+ rows) |
| [Open Data portals (NYC taxi, UK road safety)](https://data.gov.uk/) | Real-world trip/accident data to supplement |

---

## Learning Resources

| Topic | Resource |
|---|---|
| Medallion architecture & Databricks | [Databricks Lakehouse Fundamentals](https://www.databricks.com/learn) (free certification path) |
| Star schema design | Kimball's *The Data Warehouse Toolkit* (the industry bible) — or [this free summary](https://www.kimballgroup.com/data-warehouse-business-intelligence-resources/kimball-techniques/dimensional-modeling-techniques/) |
| Power BI + DAX | [SQLBI.com](https://www.sqlbi.com/) — Marco Russo & Alberto Ferrari (best DAX resources available) |
| Power Query M | [Ben Gribaudo's Power Query M Primer](https://bengribaudo.com/blog/power-query-m-primer) |
| Python ETL best practices | [Data Engineering Zoomcamp](https://github.com/DataTalksClub/data-engineering-zoomcamp) (free, project-based) |
| AWS Redshift / cloud | [AWS Free Tier + Getting Started Guide](https://aws.amazon.com/redshift/getting-started/) |
| Row-Level Security in Power BI | [Microsoft Learn — RLS](https://learn.microsoft.com/en-us/power-bi/enterprise/service-admin-rls) |

---

## What Makes This "Enterprise-Grade" vs. a Tutorial Project

- **Multiple data sources** joined together (not a single CSV)
- **Layered architecture** (bronze/silver/gold, not raw → dashboard)
- **Star schema** with proper surrogate keys and slowly changing dimensions
- **RLS in Power BI** (data permission management — explicitly in the JD)
- **Automated scheduling** (not manual notebook runs)
- **Git workflow** with branches, PRs, and commit history
- **Documentation** — architecture decisions, data dictionary, lineage

An interviewer reading this repo will see someone who thinks in systems, not scripts. That's exactly what this role demands.
