# Customer Churn Analysis (OTT Subscription Platform)

Python and SQLite analysis of subscriber churn for an OTT streaming platform. It covers data cleaning, feature engineering, 10+ KPIs, visualizations and business recommendations, built from customer, subscription and support data.

## Business Problem

In a competitive OTT market (Netflix, Hotstar, Prime), retention matters more than acquisition. The goal is to identify high-risk subscribers and answer three questions:

- **Who** left, or is likely to leave
- **Why** they left (behavior before cancelling)
- **When** the danger zone is

Churn definition used: a customer is churned if `cancellation_date` is not null.

## Tools Used

- Python (pandas, NumPy)
- SQLite (`sqlite3`)
- Matplotlib and Seaborn

## Data

Database `customer_churn`, three tables joined on `customerid`:

| Table | Key columns |
|-------|-------------|
| `db_customer` | name, country, state, gender, dob |
| `db_subscription` | subscription_start_date, renewal_date, cancellation_date, cancellation_reason, subscription_type, plan_type, contract_type, monthly_charges, cltv, churn_score |
| `db_support` | complaint_date, escalations, csat_score |

Source file: `customer_churn_data_raw.xlsx` (place it in the project folder before running the notebook).

## Approach

1. **Import**: load Excel sheets into SQLite, then read each table into pandas
2. **Clean**: rename columns, drop unused ones, fix data types, standardize gender values, fill missing country using state
3. **Feature engineering**: churn flag, complaint count per customer, tenure in days, churn risk level (low / med / high from churn score)
4. **Merge**: join the three tables, checking row counts before and after
5. **KPIs**: churn rate, retention rate, churn by plan type, ARPU, average tenure, revenue at risk, escalation rate, average complaints per customer, escalation vs churn correlation
6. **Visualize**: monthly churn trend, churn by plan and state, correlation heatmap, pairplot, catplot
7. **Pivot tables**: churn, revenue and customer count by plan type

## Key Findings

- Overall churn rate is 28.6% (retention 71.4%)
- Monthly-contract customers churn at 55.6% vs 8.3% for annual contracts
- Most churn comes from the Basic plan
- Churn peaked in September 2024, and Karnataka is the most affected state
- Churned customers account for about 18% of total monthly revenue

## Recommendations

- Investigate Karnataka and the September 2024 spike (price change, complaints, technical issues)
- Move monthly subscribers to annual contracts
- Prioritize High and Med churn-risk customers by lifetime value, and contact them through email, SMS or calls to fix their issues

## How to Run

```bash
pip install pandas numpy matplotlib seaborn openpyxl jupyter
jupyter notebook churn_analysis.ipynb
```

## Files

- `churn_analysis.ipynb`: full analysis
- `customer_churn_data_raw.xlsx`: raw dataset
- `exported_churn_data.csv`: merged dataset exported by the notebook

## Credits

Guided project from the "Churn Analysis & Customer Intelligence" course by Rishabh Mishra. Problem statement and dataset are from the course.

## Author

Alen, Data Science & Analytics graduate (2026)
