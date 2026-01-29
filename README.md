📊 ML Feature Engineering Pipeline (PySpark)
📌 Overview

This project focuses on feature engineering using PySpark to generate structured, machine-learning–ready datasets from transactional data.
The pipeline aggregates raw spending data into monthly category-level features, which can be directly used for analytics, forecasting, or ML models.

The processed features are stored in a Gold layer table, following a Medallion (Bronze–Silver–Gold) architecture.

🧠 Key Features

Extracts year and month from transaction dates

Aggregates monthly spend per category

Generates clean ML-ready features

Writes output to a Gold table for downstream ML tasks

Built using PySpark DataFrame API

🗂️ Project Structure
.
├── notebooks/
│   ├── feature_engineering.ipynb
│   └── exploratory_analysis.ipynb
├── README.md

🔧 Tech Stack

Apache Spark (PySpark)

Python

Spark SQL

Databricks / Spark-compatible environment

📐 Feature Engineering Logic

The following features are created:

year – extracted from transaction date

month – extracted from transaction date

category – spending category

monthly_category_spend – total spend per category per month

These features are aggregated and stored in a Gold table:

your_catalog.your_schema.gold_ml_features

🚀 How to Run

Set up a Spark / Databricks environment

Load the Silver-layer DataFrame (silver_df)

Run the notebook inside the notebooks/ folder

Verify the Gold table using Spark SQL

Example aggregation logic:

ml_features = (
    silver_df
    .withColumn("year", year("date"))
    .withColumn("month", month("date"))
    .groupBy("year", "month", "category")
    .agg(sum("amount").alias("monthly_category_spend"))
)

ml_features.write.mode("overwrite").saveAsTable(
    "your_catalog.your_schema.gold_ml_features"
)

📈 Use Cases

Monthly spending trend analysis

Budget forecasting

Category-level ML models

Financial analytics dashboards

🧩 Future Improvements

Add more time-based features (quarter, rolling averages)

Integrate ML models (forecasting / anomaly detection)

Add unit tests for feature validation

Automate pipeline using workflows
