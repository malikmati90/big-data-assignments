# Big Data Assignments

Coursework repository for the Big Data course. The repository contains separate assignment folders plus a shared Docker/Jupyter environment.

## Structure

- `mongodb-p1/` - Assignment 1 materials.
- `spark-pipeline-p2/` - Assignment 2 Spark pipeline notebook, instructions, and report.
- `Dockerfile`, `compose.yaml`, `requirements.txt` - shared Jupyter environment used to run the notebooks.

## Running the Environment

Start Jupyter with Docker:

```bash
docker compose up --build
```

Then open Jupyter at:

```text
http://localhost:8888
```

The container mounts this repository at `/app`, so notebooks can read files from the assignment folders directly.

## Notes

Large generated data files are ignored by Git through `.gitignore`. Recreate or download datasets from the notebooks when needed.
