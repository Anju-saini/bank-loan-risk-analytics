# Bank Loan Default & Credit Risk Analytics

A complete, end-to-end portfolio project covering SQL, Python (EDA + ML), and Tableau —
built specifically to demonstrate skills that are in high demand for Data Analyst /
Data Scientist roles in the banking & fintech domain (credit risk, NPA/collections,
loan portfolio monitoring).

## Why this project (and not something else)?
Credit risk / loan default analysis is one of the most commonly asked-about projects in
Indian banking & NBFC analytics interviews it shows you can handle the full pipeline a
bank actually cares about: messy raw data → cleaned data → risk segmentation → predictive
model → executive dashboard. It also naturally uses the exact stack already on your resume
(Python: Pandas/NumPy/Scikit-learn, SQL: MySQL/PostgreSQL, Tableau).

## File Structure
```
bank-loan-risk-analytics/
│
├── data/
│   └── loan_data.csv                    # Raw synthetic dataset (10,000 records)
│
├── sql/
│   └── 02_analysis_queries.sql          # Cleaning view + 8 analysis queries
│
├── python/
│   ├── 01_generate_data.py              # Generates the synthetic loan dataset
│   └── 02_eda_and_model.py              # EDA, cleaning, model training, exports
│
├── tableau/
│   └── TABLEAU_DASHBOARD_GUIDE.md       # Exact field/chart spec to build the dashboard
│
├── outputs/                              # Generated after running the Python scripts
│   ├── chart_default_by_credit_band.png
│   ├── chart_default_by_purpose.png
│   ├── chart_lti_boxplot.png
│   ├── chart_correlation_heatmap.png
│   ├── chart_roc_curve.png
│   ├── chart_confusion_matrix.png
│   ├── chart_feature_importance.png
│   ├── loan_data_for_tableau.csv        # Final cleaned + scored dataset → load into Tableau
│   └── model_performance_summary.csv
│
└── README.md
```

## How to run it
```bash
cd python
pip install pandas numpy scikit-learn matplotlib seaborn

python 01_generate_data.py     # creates ../data/loan_data.csv
python 02_eda_and_model.py     # creates all charts + Tableau export in ../outputs/
```
Then open Tableau and follow `tableau/TABLEAU_DASHBOARD_GUIDE.md`.

For the SQL part: load `data/loan_data.csv` into MySQL/PostgreSQL (commands are at the
top of the .sql file) and run through `sql/02_analysis_queries.sql` or just open the
CSV in any SQL-on-CSV tool (e.g. DB Browser for SQLite, or pandasql) if you don't want to
spin up a full database.

## What the project demonstrates
| Skill | Where |
|---|---|
| Data cleaning (missing values, duplicates, inconsistent text) | `02_eda_and_model.py`, SQL view |
| SQL window functions, CTEs, aggregations | `02_analysis_queries.sql` |
| EDA & storytelling with visuals | `02_eda_and_model.py` charts |
| Feature engineering (loan-to-income ratio, credit bands, DPD buckets) | both SQL & Python |
| Classification modeling (Logistic Regression + Random Forest) | `02_eda_and_model.py` |
| Model evaluation (ROC-AUC, confusion matrix, feature importance) | `02_eda_and_model.py` |
| Dashboard design or business stakeholders | `TABLEAU_DASHBOARD_GUIDE.md` |

## Results summary (on this run)
- 10,000 synthetic loan records, ~34% default rate (deliberately risk-skewed sample so
  the model has clear signal to learn from call this out as a stress-test sample if asked,
  real bank portfolios are usually 2-8% NPA)
- Logistic Regression ROC-AUC: ~0.66 | Random Forest ROC-AUC: ~0.63
- Top default drivers: credit score, loan-to-income ratio, existing loan count, loan purpose
  (Credit Card Consolidation loans riskiest; Home loans safest)

## How to talk about this in an interview
1. **Problem framing**: "Banks need to know which loans are likely to default *before*
   disbursement, and which existing loans need collections attention *now*."
2. **Data**: "I used a synthetic dataset built to mimic real loan-tape structure, with
   deliberate data quality issues missing income, duplicate records, inconsistent
   city casing so I could demonstrate real cleaning steps, not just modeling on a
   perfectly clean Kaggle CSV."
3. **Analysis**: Walk through credit band → default rate trend, loan purpose risk,
   geographic concentration.
4. **Model**: "I compared Logistic Regression for interpretability against Random Forest
   for accuracy, and used ROC-AUC plus a class-imbalance-aware metric since defaults are
   the minority class."
5. **Business impact**: "The dashboard's high-risk watchlist lets a collections team
   prioritize who to call first, and the risk segment view lets credit policy teams see
   where the portfolio's exposure is concentrated."

## Honest gaps / good next steps (worth knowing if asked)
- This uses scikit-learn, not PySpark/Databricks if a job description asks for those,
  say you'd port the same pipeline to PySpark for scale, and mention you're aware of the
  conceptual difference (distributed processing vs single-machine).
- No orchestration tool (Airflow/dbt) used here fine for a portfolio project, but worth
  acknowledging if the JD specifically asks for pipeline orchestration experience.
