# 🏠 AirBnB CDC Ingestion Data Pipeline

### Industrial Data Engineering Project

An end-to-end cloud data engineering pipeline for ingesting, transforming, modeling, and analyzing AirBnB-style customer and booking data using Azure services, CDC processing, dimensional modeling, SQL analytics, workflow automation, and AI-powered reporting.

---

## 📌 Project Overview

This project implements a modern data engineering pipeline for an AirBnB-style booking platform.

The solution integrates customer data from **Azure Data Lake Storage (ADLS)** and incremental booking events from **Azure Cosmos DB Change Feed**, processes the data using **Azure Data Factory (ADF)**, stores analytical data in **Azure Synapse Analytics**, and uses **n8n + OpenAI** to generate personalized leadership reports.

The project demonstrates practical implementation of:

- Batch data ingestion
- Incremental data ingestion
- Change Data Capture (CDC)
- SCD Type-1 processing
- Data transformation and enrichment
- Fact and dimension modeling
- SQL-based analytical aggregation
- Pipeline orchestration
- Workflow automation
- LLM-powered reporting

> **Project Status:** Completed Industrial Project / Portfolio Showcase  
> The original Azure environment is no longer accessible, so this repository documents the implemented architecture, source code, SQL logic, workflow design, and available project evidence.

---

# 🏗️ Architecture

```text
                         CUSTOMER DATA FLOW

                    ┌──────────────────────┐
                    │   Customer CSV Data  │
                    │      ADLS Gen2       │
                    └──────────┬───────────┘
                               │
                         Hourly Trigger
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Azure Data Factory │
                    │ Customer Data Pipeline│
                    └──────────┬───────────┘
                               │
                         SCD Type-1 Merge
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Azure Synapse        │
                    │    dim_customer      │
                    └──────────────────────┘


                         BOOKING DATA FLOW

                    ┌──────────────────────┐
                    │   Azure Cosmos DB    │
                    │      Bookings        │
                    └──────────┬───────────┘
                               │
                          Change Feed
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Azure Data Factory │
                    │     CDC Pipeline     │
                    └──────────┬───────────┘
                               │
                        Data Flow Processing
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Azure Synapse        │
                    │    fact_booking      │
                    └──────────┬───────────┘
                               │
                         SQL Aggregation
                               │
                               ▼
                    ┌──────────────────────┐
                    │ BookingCustomer      │
                    │ Aggregation          │
                    └──────────┬───────────┘
                               │
                               ▼
                         ┌────────────┐
                         │    n8n     │
                         └─────┬──────┘
                               │
                         Contextual Data
                               │
                               ▼
                       ┌───────────────┐
                       │   OpenAI LLM  │
                       └───────┬───────┘
                               │
                        Generated Report
                               │
                               ▼
                         ┌───────────┐
                         │  Outlook  │
                         └───────────┘
