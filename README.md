# People Data Pipeline - Databricks

This is my Data Engineering portfolio project built in Databricks using employee data.

The goal of this project was to build an end-to-end data pipeline and practice working with PySpark, Spark SQL, Delta Lake and the Medallion Architecture.

## How the project works

The pipeline starts with synthetic employee data generated in Python.

The general flow is:

Python data generator
        ↓
Bronze
        ↓
Silver
        ↓
Gold

The complete process is orchestrated using a Databricks Job.

## Architecture

![People Data Pipeline Architecture](docs/architecture.png)

## Data generator

`notebooks/generator.ipynb`

The generator creates synthetic employee data and intentionally includes some data quality issues.

Examples include:

- invalid salary values
- missing countries
- unknown employee statuses
- missing or invalid emails
- invalid hire dates
- duplicate employee IDs

These errors are later detected in the Silver layer.

## Bronze

`notebooks/bronze_ingestion.ipynb`

The Bronze layer loads the raw source data and stores it as a Delta table.

At this stage the source data is kept mostly unchanged.

## Silver

`notebooks/silver_validation.ipynb`

The Silver layer is responsible for cleaning and validating the data.

It includes:

- type casting
- date parsing
- data quality checks
- duplicate detection
- deduplication using Window functions
- reconciliation checks

After validation, records are split into:

- `employees_clean`
- `employees_rejected`
- `employees_excluded`

## Gold

`notebooks/gold_reporting.ipynb`

The Gold layer uses the clean Silver data to create reporting tables.

The project includes:

- `department_summary`
- `country_summary`
- `employment_type_summary`
- `status_summary`
- `hiring_summary`

These tables contain aggregated employee information for reporting and analysis.

## Orchestration

The full pipeline is run using a Databricks Job.

The task flow is:

generator
    ↓
bronze_ingestion
    ↓
silver_validation
    ↓
gold_reporting

Each stage runs after the previous stage completes successfully.

## Technologies used

Python, PySpark, Spark SQL, Databricks, Delta Lake, Git and GitHub.

---

Patryk Latek  
Junior Data Engineer portfolio project
