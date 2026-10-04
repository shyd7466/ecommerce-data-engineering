# E-Commerce Data Engineering Platform

## 📌 Project Overview

This project demonstrates an end-to-end data engineering platform for an
e-commerce business.

The platform ingests customer, product, order, and order-item data and
processes it through a scalable Medallion Architecture consisting of
Bronze, Silver, and Gold layers.

The objective is to build reliable, incremental, and analytics-ready
datasets while implementing data quality, deduplication, and historical
data processing.

---

## 🏢 Business Scenario

ShopSphere is an e-commerce company that receives data from multiple
operational sources.

The business needs a centralized data platform to:

- Ingest raw operational data
- Clean and validate incoming records
- Handle duplicate records
- Process incremental data
- Maintain historical changes
- Create analytics-ready datasets
- Implement data quality checks
- Support business reporting and analytics

---

## 🏗️ Architecture

```text
                    E-Commerce Sources
                           |
                           v
                    Azure Data Factory
                           |
                           v
                       ADLS Gen2
                           |
                           v
                    +-------------+
                    |   BRONZE    |
                    | Raw Data    |
                    +-------------+
                           |
                        PySpark
                           |
                           v
                    +-------------+
                    |   SILVER    |
                    | Clean Data  |
                    +-------------+
                           |
                    Business Logic
                           |
                           v
                    +-------------+
                    |    GOLD     |
                    | Analytics   |
                    +-------------+
                           |
                           v
                    SQL / Power BI