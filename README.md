# U.S. College Salary Analysis — Region × School Type

**Python · pandas · NumPy · Matplotlib · scikit-learn · Linear Regression**

A statistical exploration of how starting salary, geographic region, and institution type relate to **mid-career salary** outcomes at U.S. colleges. This notebook introduces a **region-adjusted salary uplift** measure and fits a linear model with **Region × School Type interactions**.

## Questions explored

- Which colleges have mid-career salaries above their own region's average?
- How do starting salaries vary by region and school type?
- Does combining starting salary with regional and school-type information help explain mid-career salary variation?

## Data and workflow

The notebook expects two source datasets:
- `salaries-by-college-type.csv` — college-level pay data with school type
- `salaries-by-region.csv` — college-level pay data with geographic region

It normalizes field names, parses salary values, joins schools across datasets, computes region-specific average salaries, and compares schools using:

```text
Mid-career uplift = School mid-career median salary − Region average mid-career median salary
```

The notebook then produces descriptive summaries, a top-10 uplift chart, region-by-school-type grouped means, a salary correlation matrix, a linear regression with interaction terms, and an uplift distribution plot.

## Selected results

Figures below are **recorded notebook outputs**, not a new independent validation.

| Metric | Saved result |
| --- | ---: |
| Colleges with starting and mid-career salary summaries | 269 |
| Mean starting median salary | $46,068 |
| Mean mid-career median salary | $83,932 |
| Starting-to-mid-career salary correlation | **0.89** |
| Region + School Type interaction model | **R² = 0.871** (n = 268) |

The positive correlation suggests that schools with higher starting median salaries also tended to report higher mid-career medians in this dataset. The interaction model describes **in-sample fit**, not out-of-sample prediction performance. It does **not** establish a causal effect of school type or region.

## Files

- [`college_salary_final_project.ipynb`](college_salary_final_project.ipynb) — analysis code, saved outputs, and visualizations
- [`README.md`](README.md) — overview, findings, and caveats

## Running the notebook

**Important: this repository is not yet reproducible as a fresh clone.**

1. Install Python 3 and Jupyter with `pandas`, `numpy`, `matplotlib`, and `scikit-learn`.
2. Obtain the two source CSVs listed above and place them in the notebook's working directory (they are **not** included in this repository).
3. Before running the notebook's “Setup & Data Load” cell, load the two tables into `df_type_raw` and `df_region_raw`. The current saved notebook uses those DataFrames before defining them. One way to supply the missing initialization is:

   ```python
   df_type_raw = pd.read_csv("salaries-by-college-type.csv")
   df_region_raw = pd.read_csv("salaries-by-region.csv")
   ```

   These lines must be added **after importing pandas** and **before** the first use of either variable.
4. Restart the kernel and run the remaining cells in order after correcting initialization. Notebook outputs document a previous successful analysis session, but a clean, independent run has not been verified.

## Methodological caveats

- Salary summaries are at the **college level**, not individual graduate records.
- Missing major, cohort, industry, cost-of-living, and labor-market variables limit interpretation.
- Regional baselines depend on the available schools in the source tables and the way the datasets were merged.
- R² is calculated **in sample**; no held-out predictive evaluation is documented.
- The original data sources, precise snapshot date, and reproducibility setup should be documented before treating this as a production-quality research artifact.

## Planned improvements

- Add source CSVs where redistribution is permitted, with dataset provenance and dates.
- Repair the data-loading cell and verify a clean restart-and-run.
- Export key figures into the README and add out-of-sample evaluation.
- Explain how missing regional matches and incomplete rows affect the reported model sample.

## Author

**Jihoon Lim** — undergraduate Data Science / Mathematics project.
