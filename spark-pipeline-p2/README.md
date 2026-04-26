# Assignment 2: Spark Pipeline

This folder contains the second Big Data assignment: a Spark pipeline over the 2024 NYC Yellow Taxi Trip Data.

## Contents

- `Assignment 2 - Spark Pipeline.pdf` - original assignment instructions.
- `notebook.ipynb` - completed Spark notebook with RDDs, DataFrames, SQL, window functions, and performance analysis.
- `Report-Assignment2.pdf` - final report for submission.
- `data/` - local Parquet data and generated cleaned datasets. This folder is ignored by Git.

## Notebook Sections

1. **Spark RDDs** - loads January 2024 data as an RDD and performs map/reduce-style operations.
2. **DataFrames: Cleaning and Transforming** - loads all 2024 monthly files, explores quality issues, cleans the dataset, engineers features, and writes cleaned Parquet output.
3. **Spark SQL and Window Functions** - answers analytical questions using SQL, CTEs, CASE expressions, window functions, and ROLLUP.
4. **Performance Analysis** - inspects query plans, compares cached vs uncached execution, and tests partitioned reads.
5. **Final Report** - summarizes findings and performance observations.

## Running

From the repository root:

```bash
docker compose up --build
```

Open Jupyter at:

```text
http://localhost:8888
```

Then open:

```text
spark-pipeline-p2/notebook.ipynb
```

Run the notebook from top to bottom. The Spark session is configured with `4g` driver memory and reduced shuffle partitions for local execution.

## Dataset

The notebook expects the 2024 yellow taxi Parquet files in:

```text
spark-pipeline-p2/data/
```

The required files follow this pattern:

```text
yellow_tripdata_2024-*.parquet
```

The notebook also writes cleaned outputs under `data/`, including the cleaned full-year dataset and the month-partitioned dataset used in the performance section.
