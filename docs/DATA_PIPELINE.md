# Data Pipeline

End-to-end, DVC-managed pipeline that turns raw Iris data into validated, model-ready features.

## Pipeline Stages

| Stage | Purpose | Input | Output |
|---|---|---|---|
| Collect | Obtain raw Iris data | sklearn Iris dataset | `data/raw/iris_raw.csv` |
| Preprocess | Clean data (drop duplicates, impute missing values) | `iris_raw.csv` | `data/processed/iris_preprocessed.csv` |
| Feature Engineering | Create useful features | `iris_preprocessed.csv` | `data/processed/iris_features.csv` |
| Validate | Check schema, nulls and ranges | `iris_features.csv` | Validation result (exit code 0 or 1) |

## Validation Rules (validate.py)

- All expected columns are present (4 measurements, `species`, `sepal_area`, `petal_area`, `sepal_to_petal_length_ratio`, `petal_length_bin`)
- No null values in any column
- `species` is one of: setosa, versicolor, virginica
- Range checks:
  - sepal length: 3.0 to 9.0 cm
  - sepal width: 1.5 to 5.5 cm
  - petal length: 0.5 to 8.0 cm
  - petal width: 0.05 to 3.0 cm

On any failure the stage logs each error and exits with code 1, halting the pipeline.

## Flow Diagram

```
collect --> preprocess --> features --> validate
   |            |             |            |
iris_raw   iris_preprocessed  iris_features  (pass/fail)
 .csv           .csv            .csv
```

## How to Run

```
dvc repro     # run the full pipeline (only changed stages re-run)
dvc dag       # show the stage dependency graph
dvc push      # push data artifacts to the DVC remote
```