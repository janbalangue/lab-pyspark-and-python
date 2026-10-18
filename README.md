# Lab: Pyspark and Python

A Jupyter notebook lab that uses PySpark and pandas to explore the Wisconsin Diagnostic Breast Cancer dataset. It walks through a basic big-data workflow from start to finish: start a Spark session, load and inspect the data, compute summary statistics, plot the class balance, and shut Spark down.

## Contents

| File | Description |
| --- | --- |
| `CGLabC4M3.ipynb` | The lab notebook, with one code cell per step (graded with CodeGrade) |
| `breast_cancer.csv` | The dataset: 569 patients, each with an ID, a diagnosis (`M` = malignant, `B` = benign) and 30 numeric features |

## Dataset

Each row describes cell nuclei measured from a digitized image of a fine needle aspirate (FNA) of a breast mass. For ten characteristics (radius, texture, perimeter, area, smoothness, compactness, concavity, concave points, symmetry and fractal dimension), the dataset records the mean, the standard error (`_se`) and the "worst" value (`_worst`).

The data comes from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic). Every line in this copy of the CSV ends with a trailing comma, so Spark reads an extra empty column named `_c32`. That column is why the notebook reports 33 columns instead of 32.

## Steps

| Step | Task | Result |
| --- | --- | --- |
| 1 | Create a Spark session named "Breast Cancer Analysis" and confirm it is active | `yes` |
| 2 | Load the CSV into a Spark DataFrame and convert it to pandas | `df_pandas` |
| 3 | Show the schema and the first few records, then count rows and columns | 569 rows, 33 columns |
| 4 | Select the 50th row and its `radius_mean` | 13.49 |
| 5 | Count malignant and benign diagnoses and take the difference (M − B) | 212 − 357 = −145 |
| 6 | Plot the relative frequency of each diagnosis | Malignant ≈ 0.3726 |
| 7 | Absolute difference between the max `fractal_dimension_mean` and the min `symmetry_mean` | 0.0086 |
| 8 | Product of the benign means of `radius_mean`, `texture_mean` and `perimeter_mean` | 12.15 × 17.91 × 78.08 ≈ 16990.72 |
| 9 | Mean ratio of `radius_mean` to `perimeter_mean` for malignant cases | 0.15 |
| 10 | Stop the Spark session and confirm it is closed | `yes` |

The grading rubric also asks for a few things that the step instructions don't. Each one is in an extra cell (with no CodeGrade tag) right after the matching step:

| After step | Rubric item | Result |
| --- | --- | --- |
| 3 | Perimeter mean of the 77th row (`perimeter_mean_value`) | 87.91 |
| 5 | Difference of the counts as B − M (`b_minus_m`) | 357 − 212 = 145 |
| 7 | The same max and min, computed with `max` and `min` from `pyspark.sql.functions` | Matches pandas (0.0086) |
| 8 | Sum of the benign standard deviations of `radius_mean`, `texture_mean` and `perimeter_mean` (`std_sum_b`) | 1.78 + 4.00 + 11.81 = 17.59 |

## Running the notebook

Requirements:

- Python 3
- Java 17 or later (PySpark runs on the JVM)
- `pyspark`, `pandas`, `numpy`, `matplotlib` and `jupyter`

```bash
pip install pyspark pandas numpy matplotlib jupyter
jupyter notebook CGLabC4M3.ipynb
```

Run all cells from top to bottom (**Kernel → Restart & Run All**). Later steps reuse `spark_df` and `df_pandas` from earlier cells, and Step 10 stops the Spark session, so it must run last. The notebook expects `breast_cancer.csv` to be in the same folder.
