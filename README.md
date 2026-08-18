Project XYZ

**Project XYZ** is a comprehensive data analysis tool designed to streamline data exploration, analysis, and visualisation. The tool supports multiple data formats and provides an intuitive interface for both novice and expert data scientists.

# ![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)

## Dataset Content

* The dataset I used was the Synthetic Fraud Dataset from Kaggle. Here is this link for the Dataset: https://www.kaggle.com/datasets/samayashar/fraud-detection-transactions-dataset 

## Business Requirements

* Identify which transaction, behavioural and risk-score features are significantly associated with fraud.
* Determine whether commonly assumed risk factors such as transaction type, location and time of day/weekend actually influence fraud rate or whether fraud risk is instead concentrated in a small number of stronger behavioural signals.
* Build and compare classification models to determine whether combining risk indicators improves fraud prediction over relying on any single indicator alone.
* Present findings through visualisations

## Hypothesis and how to validate?

H1: Transactions with more failed attempts in the past 7 days are more likely to be fraudulent
* Validation: Compare Failed Transaction Count 7d between fraudulent and non-fraudulent transactions using a box plot and t-test

H2: Transactions with a higher risk score are more likely to be fraudulent
* Validation: Compare Risk Score between fraudulent and non-fraudulent transactions using a box plot and t-test

H3: Combining risk score and failed transaction count predicts fraud more accurately than either alone
* Validation: Compare model performance (AUC/precision-recall) using each feature individually vs combined

H4: Certain transaction types are more commonly associated with fraud
* Validation: Analyse fraud rates by transaction type using a bar chart

H5: Certain locations have a higher incidence of fraud compare to others
* Validation: Analyse fraud rates by location using a bar chart

H6: Fraud is more likely to occur at certain times of the day or on weekends
* Validation: Analyse fraud rates by hour of the day and weekend status using a time series/line chart
## Project Plan

* Explore the raw dataset, assessed data quality, and identified which features were relevant to the business requirements.
* ETL: Clean the raw data check for missing values, duplicates, incorrect data types, and outliers and engineer new features (e.g. hour of day and day of week from the transaction timestamp).
* EDA: Analyse distributions and relationships between features and fraud, and tested six hypotheses using statistical methods (t-tests and chi-square tests).
* Data Visualisation: Create plots mapped to each hypothesis and business requirement, and built an interactive Tableau dashboard for further exploration.
* Modelling:  Build and compare two classification models (Logistic Regression and Random Forest) to predict fraud, using the features identified as significant during EDA.

## The rationale to map the business requirements to the Data Visualisations

* List your business requirements and a rationale for mapping them to the Data Visualisations
