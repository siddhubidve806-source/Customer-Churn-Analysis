Customer Churn Analysis — Siddhesh
Project Overview
This project analyzes customer subscription and support data to understand customer churn, retention, revenue exposure, customer tenure, complaints, escalations, and churn-risk segments.

The workflow combines SQLite database tables with Python-based data cleaning, feature engineering, exploratory data analysis (EDA), visualization, correlation analysis, and summary tables.

Project Objectives
Identify churned and retained customers.
Calculate churn rate and retention rate.
Compare churn across subscription plan types and states.
Estimate average revenue per user (ARPU).
Calculate customer tenure.
Estimate monthly revenue at risk from churned customers.
Analyze complaint counts, escalations, and their relationship with churn.
Categorize customers into low, medium, and high churn-risk groups using churn_score.
Produce charts, correlation heatmaps, categorical comparisons, and pivot tables.
Dataset and Files
The project uses the following local files:

File	Description
siddhesh_churn_analysis.ipynb	Main Jupyter Notebook containing the complete analysis workflow
customer_churn.db	SQLite database containing customer, subscription, and support tables
exported_churn_data.csv	Final merged dataset exported from the notebook
Dataset link: The repository-relative dataset files are exported_churn_data.csv and customer_churn.db. The original Excel source path used in the notebook was local to the author's computer and no public source URL was included in the supplied notebook.

Database Structure
The SQLite database contains these tables:

Table	Rows	Purpose
db_customer	21	Customer profile information such as name, country, state, gender, date of birth, interests, and pincode
db_subscription	21	Subscription, plan, contract, cancellation, monthly charges, CLTV, and churn score
db_support	9	Complaint date, escalation status, CSAT score, and support comments
The exported CSV contains 21 rows and 23 columns after merging the tables and engineering features.

Technology Used
Python — core programming language
Pandas — data loading, cleaning, transformation, merging, grouping, and pivot tables
NumPy — conditional feature engineering and numerical operations
Matplotlib — charts and correlation heatmap visualization
Seaborn — heatmaps and categorical multi-dimensional plots
SQLite3 — database connection and SQL-based table access
Jupyter Notebook / VS Code Notebook — interactive development and analysis
Processing Workflow
Connect to the SQLite database.
Read database tables into Pandas DataFrames.
Inspect data using head(), tail(), and info().
Clean and standardize customer data, including date conversion, gender labels, and missing country values.
Convert subscription and complaint date columns to datetime.
Remove unnecessary support columns and reduce support records to one record per customer while calculating complaint count.
Create churn_flag:
1 when cancellation_date is available.
0 when cancellation_date is missing.
Merge subscription, customer, and support data using customerid.
Export the merged dataset to exported_churn_data.csv.
Perform EDA, visualizations, correlation analysis, and pivot-table analysis.
Main Features and KPIs
Churn Rate: percentage of customers with churn_flag = 1.
Retention Rate: 100 - churn_rate.
Churn Rate by Plan: average churn flag grouped by plan_type.
ARPU: mean of monthly_charges.
Average Tenure: number of days between subscription start and cancellation, or between subscription start and the current date for active customers.
Revenue at Risk: sum of monthly_charges for churned customers.
Escalation Rate: percentage of records where escalations == 'Y'.
Average Complaints per User: total complaint count divided by unique customers.
Escalation–Churn Correlation: correlation between encoded escalation values and churn_flag.
Churn Risk: based on churn_score:
Low: score below 50
Medium: score from 50 to below 70
High: score 70 or above
Visualizations Included
Monthly churn trend
Churn rate by plan type
Churn rate by state
Correlation heatmap
Categorical comparison of plan type, monthly charges, gender, and churn risk
Pivot tables for plan-level churn, revenue, and customer counts
Run Instructions
1. Clone or copy the project
Place the following files in the same project directory:

siddhesh_churn_analysis.ipynb
customer_churn.db
exported_churn_data.csv
2. Create a virtual environment
Windows:

python -m venv env
env\Scripts\activate
macOS/Linux:

python3 -m venv env
source env/bin/activate
3. Install dependencies
pip install -r requirements.txt
4. Open the notebook
jupyter notebook siddhesh_churn_analysis.ipynb
Or open the notebook in VS Code with the Jupyter extension.

5. Execute the notebook
Run the cells from top to bottom. If you want to recreate the database import step, update the original Excel file path in the notebook to match your own machine.

Important Notes and Limitations
The supplied notebook references an original Excel file using a local Windows path. That file was not included in the supplied project package.
The notebook uses pd.Timestamp.today() when calculating tenure for active customers, so the resulting tenure can change when the notebook is run on a different date.
The support table is reduced to one latest complaint record per customer after calculating complaint_count.
Correlation does not establish causation.
The project is an exploratory analytics workflow; it does not train or deploy a machine-learning churn prediction model.
Check column names and file paths before running the notebook on another computer.
Suggested Business Use
The analysis can help a subscription business identify customer segments with elevated churn, monitor retention performance, prioritize customer-support improvements, review revenue exposure, and design targeted retention campaigns. Any business action should be validated using additional data and controlled measurement.

Author
Siddhesh

License
Add a license appropriate for your repository before publishing publicly.
