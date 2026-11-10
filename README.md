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

## Findings and validation

The old `R² = 0.871` reported in the original notebook was **in-sample**, not evidence of predictive generalization. It has been removed from the headline claims. Run the revised notebook to see baseline vs interaction-model performance on held-out schools. The refactored notebook intentionally has **no cached results** and has **not yet been independently re-executed on the source CSVs**.

## Interpretation limits

- Historical, **school-level** summary values do not predict a particular person's salary.
- Associations among school type, region, and salary are **not causal**. Confounding factors include major, student selection, cohort, industry, and experience.
- Region lookups depend on exact school-name matches. Some schools might have no matching region and will be excluded from predictive modeling.
- A small held-out sample produces uncertain performance estimates; this is a learning portfolio project, not a deployed predictive service.

**Author:** Jihoon Lim. Original student project, subsequently revised for reproducibility and better out-of-sample evaluation.
