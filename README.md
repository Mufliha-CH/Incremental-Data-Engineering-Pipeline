# Incremental Data Engineering Pipeline Using Databricks

## Project Overview

This project implements an incremental data engineering pipeline using **Databricks, PySpark, Spark SQL and Delta Lake**.

The pipeline processes incoming order data from multiple CSV batches, validates records, removes duplicates, handles late-arriving data and maintains data across Bronze, Silver and Gold layers.

It also includes batch tracking, audit logging and notebook automation to support reliable and repeatable data processing.

## Problem Statement

Processing large datasets repeatedly can lead to duplicate records, unnecessary computation and inconsistent results.

The objective of this project is to build an incremental pipeline that processes only new or unprocessed batches while maintaining data quality, historical consistency and reliable execution.

## Technologies Used

- Databricks Free Edition
- Python
- PySpark
- Spark SQL
- Delta Lake
- Unity Catalog
- CSV

## Pipeline Architecture

The project follows the Medallion Architecture.

**1. Bronze Layer – Raw Data**

- Ingests incoming CSV batch files.
- Stores raw order records.
- Maintains source information for traceability.

**2. Silver Layer – Cleaned Data**

- Validates incoming records.
- Identifies invalid records.
- Removes duplicates using business keys.
- Handles incremental updates using Delta MERGE.
- Supports late-arriving records.

**3. Gold Layer – Business Data**

- Creates summarized order data.
- Aggregates order information by status.
- Provides data for reporting and analysis.

## Data Quality and Error Handling

The pipeline includes:

- Required field validation.
- Data type validation.
- Duplicate record handling.
- Invalid record separation.
- Quarantine table for rejected records.
- Audit logging for pipeline execution.

## Incremental Processing

The pipeline uses Delta Lake MERGE to update existing records and insert new records.

A processed batches tracking table records successfully completed batches.

This helps prevent successfully processed files from being processed again unnecessarily and supports safe reruns.

## Automation

The project uses two Databricks notebooks:

**Incremental_Pipeline_Final**

Responsible for:
- Reading CSV files.
- Data validation.
- Bronze ingestion.
- Silver transformations.
- Gold table generation.
- Audit and batch tracking.

**Incremental_Pipeline_Automation**

Responsible for:
- Discovering CSV files in the Volume.
- Identifying unprocessed files.
- Generating batch IDs.
- Triggering the main pipeline notebook.
- Capturing execution results.

## Tables Used

| Table | Purpose |
|---|---|
| bronze_orders | Raw order records |
| silver_orders | Cleaned and processed orders |
| gold_orders_summary | Aggregated order data |
| quarantine_orders | Invalid records |
| pipeline_audit | Pipeline execution details |
| processed_batches | Batch processing status |

## Project Structure

```text
Incremental-Data-Engineering-Pipeline/
│
├── notebooks/
│   ├── Incremental_Pipeline_Final.ipynb
│   └── Incremental_Pipeline_Automation.ipynb
│
├── sample_data/
│   ├── batch_1.csv
│   ├── batch_2.csv
│   └── batch_3.csv
│
└── README.md
```

## Execution Workflow

1. Upload CSV batch files to the Databricks Volume.
2. Run the Automation notebook.
3. Discover incoming CSV files.
4. Identify files that have not been successfully processed.
5. Generate batch IDs.
6. Execute the main pipeline notebook.
7. Validate and ingest data into Bronze.
8. Clean and merge records into Silver.
9. Generate Gold summaries.
10. Record audit and batch processing information.

## Testing and Validation

The pipeline is designed to support the following test scenarios:

- Initial batch processing.
- Processing new incoming batches.
- Duplicate record handling.
- Invalid data handling.
- Late-arriving data.
- Reprocessing previously completed batches.
- Data reconciliation across layers.

## Learning Outcomes

Through this project, I gained practical experience in:

- Building data pipelines using PySpark.
- Implementing Medallion Architecture.
- Working with Delta Lake.
- Performing incremental data processing.
- Using Delta MERGE operations.
- Implementing data validation and deduplication.
- Handling late-arriving records.
- Automating Databricks notebooks.
- Implementing batch tracking and audit logging.

## Future Improvements

- Implement file-arrival-based triggering.
- Add pipeline monitoring and alerting.
- Improve failure recovery and retry handling.
- Extend the pipeline to support larger datasets.

## Conclusion

This project demonstrates the implementation of an incremental data engineering pipeline using Databricks and Delta Lake. It combines data ingestion, transformation, validation, incremental processing and automation to build a reliable batch-processing solution.
