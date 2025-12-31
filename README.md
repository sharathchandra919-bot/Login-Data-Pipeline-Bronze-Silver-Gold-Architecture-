# Login-Data-Pipeline-Bronze-Silver-Gold-Architecture-

📖 Project Overview

This project demonstrates an end-to-end data engineering pipeline built using Apache Spark, following the Bronze–Silver–Gold data architecture pattern.

The pipeline processes raw social media usage data, cleans and deduplicates it, applies data quality checks, and produces business-ready analytical metrics such as engagement vs satisfaction.

🎯 Problem Statement

Raw user activity data often contains:

inconsistent column naming

duplicate records

invalid or incomplete time information

noisy fields unsuitable for analytics

The goal of this pipeline is to transform untrusted raw data into reliable business insights using production-style data engineering practices.

🧱 Architecture Overview
Raw CSV
  ↓
Bronze Layer
  ↓
Silver Layer
  ↓
Gold Layer
  ↓
Business Insights

🥉 Bronze Layer — Raw Ingestion

Purpose: Preserve raw data for traceability.

Responsibilities:

Read raw CSV data

Infer schema

No cleaning or transformations

📌 Principle: “Bronze data is immutable and untrusted.”

🥈 Silver Layer — Clean & Trusted Data

Purpose: Create reliable, analytics-safe data.

Key Transformations:

Column standardization (snake_case)

Time-of-day validation (without fabricating timestamps)

Business-key based deduplication

Data quality checks (nulls, ranges, sanity checks)

Deduplication Strategy:

Records are deduplicated using business keys:

user_id

platform

video_id

watch_time_of_day

📌 Production rule followed:

Never fabricate missing timestamps. Preserve raw truth.

🥇 Gold Layer — Business Metrics

Purpose: Provide aggregated insights for analytics and decision-making.

Implemented Metrics:

Engagement vs Satisfaction Analysis

Average satisfaction by engagement level

User counts for statistical context

Gold Table Characteristics:

Aggregated, stable schema

Business-friendly

Includes audit fields (created_at)

✅ Data Quality Checks

To ensure trust in metrics, the pipeline enforces:

Null percentage thresholds

Valid numeric ranges

Deduplication sanity checks

Row count consistency between layers

📌 Philosophy:

Failing loudly is better than producing silent wrong metrics.

🛠️ Technologies Used

Apache Spark (PySpark)

Python

Google Colab (Linux execution)

draw.io (architecture diagram)

🧠 Key Learnings

Practical application of Bronze–Silver–Gold architecture

Deterministic deduplication using business keys

Handling incomplete temporal data without violating data integrity

Designing Gold metrics aligned with business questions

Communicating pipeline design clearly for interviews

