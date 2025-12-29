# FMCG Analytics — Databricks (Free Edition) Notebooks (S3-backed data)

A curated collection of Databricks-compatible Jupyter/Databricks notebooks for exploratory data analysis, visualization, forecasting and modeling in the Fast-Moving Consumer Goods (FMCG) domain. This repository is prepared to run on Databricks Free Edition and expects all datasets to be stored in AWS S3.

Use this README to import notebooks into Databricks, configure secure access to S3, run on a free cluster, and save reproducible outputs (Delta / MLflow) back to S3.

> NOTE: Replace placeholder names (S3 bucket, Databricks secret scope, contact, license) with your actual values before publishing.

---

Table of contents
- Repository overview
- Quick start on Databricks Free Edition
  - Import notebooks
  - Create a cluster
  - Install libraries
- Reading and writing data (PySpark)
- Databricks CLI & Git integration
- Project structure & best practices
- Reproducibility & environment
- Contributing, license, contact

---

Repository overview
This repository contains modular notebooks for common FMCG workflows:
- data ingestion & EDA
- feature engineering
- time-series forecasting and evaluation
- promotion and price-elasticity analysis
- dashboards & visualizations

Notebooks are stored as `.ipynb` files and designed to be imported into Databricks Workspace or used via Databricks Repos.

---

Quick start on Databricks Free Edition

1. Sign in to Databricks Community Edition (https://community.cloud.databricks.com).
2. Import the notebooks:
   - Workspace UI: Workspace > Home > (your folder) > Import > Upload the `.ipynb` files.
   - Or use Databricks Repos to clone this GitHub repository (recommended for two-way sync).
3. Create and start a Free cluster:
   - Compute > Create Cluster > select a suitable Databricks Runtime with Python 3.x.
   - Note: Free clusters are ephemeral; persist outputs to S3.
4. Attach a notebook to the running cluster and run cells top-to-bottom.

Install required Python libraries in a notebook cell (preferred in Databricks)
---

Reading and writing data (Spark)

Spark examples (preferred for large datasets):
```python
# Read CSV from S3 into a Spark DataFrame
spark_df = spark.read.option("header", True).option("inferSchema", True).csv("s3a://my-bucket/path/to/sales.csv")

# Write as Delta back to S3
spark_df.write.format("delta").mode("overwrite").save("s3a://my-bucket/processed/sales_delta/")
```
Reading Parquet:
```python
spark_df = spark.read.parquet("s3a://my-bucket/path/to/data.parquet")
```
Project structure:
(All notebooks are in .ipynb format and dashboard file in .json)

-consolidated_pipeline/
  -1_Setup/(notebooks)
    -dim_date_table_creation
    -Setup_catalogs_schemas
    -utilities
  -dimension_data_processing/(notebooks)
    -customer_data_processing
    -pricing_data_processing
    -product_data_processing
  -fact_data_processing/(notebooks)
    -full_load_fact
    -incremental_load_fact
  -fmcg_dashboard/
    -Atlikon_sales_insights

Tip: keep notebooks small and focused for faster runs on Free Edition clusters.

---

Best practices for Databricks Free Edition + S3

- Use small sample datasets while developing; use full S3 data only when needed.
- Avoid storing credentials in notebooks or GitHub — use Databricks secrets / IAM roles.
- Save intermediate artifacts (Delta/Parquet) and model outputs to S3.
- Stop clusters when idle to avoid session timeouts and resource limits.
- Use `%run` to share utility notebooks (e.g., configuration, helper functions).
- Document runtime and dependency versions in notebooks and README.

---

Contact
- Maintainer: amank1510 — https://github.com/amank1510
- Email: amank0639@gmail.com

---

Acknowledgements
- Built for FMCG forecasting and retail analytics workflows.
- Leverages Databricks notebooks, S3 for storage, Delta Lake for robust data outputs, and MLflow for experiment tracking.
