# BigData_Project2

A Big Data coursework project (University of Macedonia, Applied Informatics) analyzing customer churn for a telecom provider using a 10,000-record dataset (telecom_churn_10k.csv), built entirely with PySpark (DataFrame API, Spark SQL, and Spark ML).

Overview

The project is organized into 3 parts:


Data Loading, Inspection & Cleaning

Loaded the dataset into a Spark DataFrame with schema inference and profiled missing values across all columns (300 missing values found in AGE, TENURE_MONTHS, MONTHLY_CHARGES, TOTAL_CHARGES, and the target CHURN).
Applied a targeted cleaning strategy: dropped rows with missing CHURN (the target variable can't be imputed), and used median imputation for missing numerical fields, since the median is more robust to outliers than the mean.
Ran descriptive statistics comparing active vs. churned customers, and engineered 3 new features: NUM_SERVICES, IS_LONG_TENURE, and AVG_CHARGE_PER_MONTH.



Analysis with Spark SQL

Queried the cleaned data (registered as a temp view) to confirm key churn drivers:

Contract type: month-to-month customers churn at 53.21%, vs. 20.61% (one-year) and 13.65% (two-year), short commitment strongly correlates with churn.
Number of services: customers with only 1 service churn at 47.98%, dropping to 26.84% for those with 3+ services, bundling increases retention.
Monthly charges: churned customers pay more on average (€37.01 vs. €36.25), a secondary but consistent factor.
Geography: highest churn rates were in Italy (40.78%), Germany (37.03%), the UK (36.15%), and Spain (36.10%), among countries with at least 100 customers.






Monthly Charge Prediction with a Decision Tree (Spark ML)

Built a full Spark ML Pipeline (StringIndexer → OneHotEncoder → VectorAssembler → DecisionTreeRegressor) to predict MONTHLY_CHARGES from customer and contract features.
Trained on a 70/30 split; evaluated with RMSE (€7.86) and R² (≈0.41), a reasonable fit for indicative "what-if" pricing scenarios, though not precise enough for fully automated pricing.





Tech Stack


PySpark: DataFrame API, Spark SQL, Spark ML (Pipeline, StringIndexer, OneHotEncoder, VectorAssembler, DecisionTreeRegressor, RegressionEvaluator)
Pandas: auxiliary formatting/inspection
Run in Google Colab


Repository Contents


telecom_churn_hw2.py  (full script (data cleaning, Spark SQL analysis, ML pipeline))
telecom_churn_10k.csv ( input dataset)
Report (PDF) with full write-up, business interpretation, and results


Key Takeaway

Contract length and number of subscribed services are the strongest predictors of churn, short-term contracts and single-service customers are the highest-risk segments, with monthly charges acting as a secondary factor. The Decision Tree model shows these features carry real predictive signal for pricing, useful for exploratory analysis even though it isn't precise enough to fully automate billing decisions.

Authors

Theodora Stamoglou

Georgiana Petridou


Coursework project (2nd assignment) for the Big Data module, Applied Informatics, University of Macedonia. Supervisor: Dr. Asimina Dimara.
