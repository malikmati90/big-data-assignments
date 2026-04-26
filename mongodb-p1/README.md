# Big Data Assignment 1 — Data Formats, Storage Optimization, and MongoDB

This repository contains the implementation of **Assignment 1** for the Big Data course.
The goal of this assignment is to explore different data formats, analyze their performance characteristics, and understand how storage strategies affect analytical workloads.

The assignment uses the **NYC Yellow Taxi Trip dataset (January–March 2024)** and performs experiments related to:

* Data exploration
* MongoDB document storage
* Format comparison (Parquet, CSV, JSON Lines)
* Compression benchmarking
* Column pruning
* Dataset partitioning
* Metadata inspection

The experiments are implemented in a **Jupyter Notebook** and executed inside a **Docker environment**.

---

# Dataset

The dataset comes from the **NYC Taxi & Limousine Commission (TLC)**.

Taxi trip records are provided in **Parquet format**.

Files used:

* `yellow_tripdata_2024-01.parquet`
* `yellow_tripdata_2024-02.parquet`
* `yellow_tripdata_2024-03.parquet`

These files are downloaded automatically from:

```
https://d37ci6vzurychx.cloudfront.net/trip-data/
```

Each row represents a taxi trip and includes information such as:

* pickup and dropoff timestamps
* passenger count
* trip distance
* fare amount
* tip amount
* payment type

---

# Project Structure

```
.
├── compose.yaml
├── Dockerfile
├── requirements.txt
├── notebook.ipynb
│
├── data/
│   └── parquet taxi datasets
│
├── exports/
│   ├── csv/
│   ├── json/
│   ├── parquet_compressed/
│   ├── partitioned_by_month/
│   └── partitioned_by_day/
│
└── report/
    └── final_report.pdf
```

Explanation:

* **notebook.ipynb** → main assignment implementation
* **data/** → raw Parquet datasets
* **exports/** → generated files during experiments
* **report/** → final summary report

---

# Environment Setup

The project runs entirely using **Docker**. You can also run the notebook separately if you have jupyter notebook installed.

## Build the environment

```
docker compose build
```

## Start the environment

```
docker compose up
```

Then open Jupyter in your browser:

```
http://localhost:8888
```

The notebook will appear in the root directory.

---

# Python Dependencies

The project uses the following libraries:

```
pyarrow
duckdb
pandas
jupyter
```

These are installed automatically through `requirements.txt`.

---

# Notebook Sections

The notebook follows the structure required by the assignment.

## 1. Getting to Know the Data

* Inspect Parquet files
* Count rows
* Explore schema
* Display sample records

---

## 2. MongoDB — Semi-Structured Data

A sample of **100,000 rows** is exported to **JSON Lines** and imported into MongoDB.

Queries performed:

* Count documents
* Trips with more than 4 passengers
* Average tip amount grouped by payment type
* Top 5 longest trips

This section demonstrates how document databases handle tabular data.

---

## 3. Format Comparison

Experiments comparing storage formats:

* Parquet
* CSV
* JSON Lines

Metrics analyzed:

* file size
* read performance
* format efficiency

---

## 4. Compression Benchmark

The dataset is written using different Parquet compression algorithms:

* Snappy
* Gzip
* Zstd
* No compression

Measured metrics:

* file size
* write time
* read time

Example results:

| Compression | Size (MB) | Write Time | Read Time |
| ----------- | --------- | ---------- | --------- |
| gzip        | 142.94    | 117s       | 1.29s     |
| zstd        | 151.07    | 9.51s      | 0.85s     |
| snappy      | 186.36    | 28.46s     | 0.97s     |
| none        | 238.29    | 8.08s      | 0.70s     |

Key takeaway: **Zstd provides a strong balance between compression and performance.**

---

## 5. Column Pruning

Test comparing:

* reading all columns
* reading only required columns

Query used:

```
average tip amount per payment type
```

Result: reading only required columns significantly reduces read time because **Parquet is a columnar format**.

---

## 6. Partitioning Strategy

The dataset is partitioned using **pickup month** extracted from `tpep_pickup_datetime`.

Partition example:

```
pickup_month=1/
pickup_month=2/
pickup_month=3/
```

Experiments include:

* partition inspection
* partition pruning
* over-partitioning by day

Conclusion: **month is a better partition column than day** for this dataset.

---

## 7. Metadata Inspection

Parquet metadata is inspected to analyze:

* number of row groups
* column statistics (min/max values)
* how query engines skip irrelevant data using metadata

This demonstrates how Parquet improves query performance.

---

# Key Findings

Main observations from the experiments:

* **Parquet is significantly more efficient than CSV or JSON for analytical datasets.**
* **Column pruning reduces unnecessary data reads and improves performance.**
* **Compression algorithms involve trade-offs between storage size and CPU cost.**
* **Partitioning can greatly improve query performance through partition pruning.**
* **Over-partitioning can create too many small files and reduce efficiency.**

---

# Author

Student: *Malik Sattar Malik*
Course: Big Data
Assignment: Data Formats, Storage Optimization and MongoDB

