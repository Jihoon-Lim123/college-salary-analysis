# U.S. College Salary Analysis — Region × School Type

**Python · pandas · NumPy · Matplotlib · scikit-learn · Linear Regression · Ridge**

This notebook explores historical U.S. college-level starting and mid-career salary summaries from the **Wall Street Journal / PayScale** data. It compares college salaries with regional averages and evaluates whether region and school type improve *out-of-sample* predictions of mid-career median salaries.

## What the project does

- Loads the original school-type and region CSVs (local files first, otherwise an attributed public mirror).
- Cleans column names, salary strings (e.g., `"$50,000"`), and missing data.
- Joins school-type summaries to region labels and computes historical region-adjusted salary **uplift**.
- Visualizes the top 10 school uplifts, region × school-type starting salaries, and uplift distribution.
- Compares a **starting-salary baseline** against a **Ridge regression with region, school type, and Region × Type interaction**.
- Reports **train R², 25% held-out test R² and test MAE**, plus 5-fold cross-validation on training data only. All preprocessing occurs inside scikit-learn Pipelines and is fitted only on training folds.

## Quick start

```bash
git clone https://github.com/Jihoon-Lim123/college-salary-analysis.git
cd college-salary-analysis
python -m pip install -r requirements.txt
jupyter notebook college_salary_final_project.ipynb
```

Select **Run All**. If the CSVs are not present beside the notebook, `pandas.read_csv` downloads them from the public dataset mirror below (internet required). Alternatively download both files manually and put them next to the notebook.

- [salaries-by-college-type.csv](https://github.com/UBC-MDS-2018-19/DSCI_522_Salary-vs-College/blob/master/data/raw_data/salaries-by-college-type.csv)
- [salaries-by-region.csv](https://github.com/UBC-MDS-2018-19/DSCI_522_Salary-vs-College/blob/master/data/raw_data/salaries-by-region.csv)

Data attribution: historical **Wall Street Journal / PayScale** college-salary data, mirrored by [UBC-MDS-2018-19](https://github.com/UBC-MDS-2018-19/DSCI_522_Salary-vs-College). **Exact snapshot year is not established.** Check usage and redistribution rights before republishing the original datasets; this repository fetches them rather than bundling copies.

## Files

- `college_salary_final_project.ipynb`: cleaning, descriptive summaries, visualizations, modeling, evaluation
- `requirements.txt`: Python dependencies
- `.gitignore`: ignores caches and generated `outputs/`
- `outputs/college_salary_master_with_regionavg.csv`: generated after running; not committed

## Verified modeling results

The notebook was **successfully executed end to end on GitHub Actions** with a fresh Python 3.11 environment and the historical CSV source data. The run used 268 complete school records, with 201 schools for training and 67 held out for testing (`random_state=42`).

| Model | Training R² | Held-out test R² | Held-out test MAE |
| --- | ---: | ---: | ---: |
| Starting salary only (Linear Regression) | 0.78 | 0.84 | $4,322 |
| Starting salary + Region × School Type (Ridge) | 0.87 | **0.85** | $4,366 |

The Ridge model achieves slightly higher held-out R² but **worse MAE** than the simpler model. The results do not demonstrate a clear practical advantage from adding region and school type. Training-only 5-fold CV for the Ridge model produced R² **0.839 ± 0.036**. All figures are rounded to the precision shown in the verified execution.

The previously quoted **R² = 0.871 was an in-sample score** and should not be described as predictive performance. The revised notebook intentionally has no cached outputs, so reviewers can reproduce the numbers by running **Run All**; the [successful notebook execution and downloadable executed notebook](https://github.com/Jihoon-Lim123/college-salary-analysis/actions/runs/42769639061) are also available from GitHub Actions (artifact retention: 7 days).

The reported metrics depend on one randomized hold-out split. They describe a small **historical college-level dataset**, not a causal effect or present-day individual salary predictions.

## Interpretation limits

- Historical, **school-level** summary values do not predict a particular person's salary.
- Associations among school type, region, and salary are **not causal**. Confounding factors include major, student selection, cohort, industry, and experience.
- Region lookups depend on exact school-name matches. Some schools might have no matching region and will be excluded from predictive modeling.
- A small held-out sample produces uncertain performance estimates; this is a learning portfolio project, not a deployed predictive service.

**Author:** Jihoon Lim. Original student project, subsequently revised for reproducibility and better out-of-sample evaluation.
