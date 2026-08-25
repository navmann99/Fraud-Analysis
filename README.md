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
* Result: Rejected H0 (p < 0.001)
* Summary: Fraudulent transactions have a noticeably higher average number of failed transactions in the past 7 days (mean 3.05, median 4) compared to genuine transactions (mean 1.51, median 2). Transactions with 4 or more failed attempts are fraudulent 100% of the time in this dataset, suggesting a practical threshold for flagging accounts.

H2: Transactions with a higher risk score are more likely to be fraudulent
* Validation: Compare Risk Score between fraudulent and non-fraudulent transactions using a box plot and t-test
* Result: Rejected H0 (p < 0.001)
* Summary: Fraudulent transactions have a noticeably higher risk score on average (mean 0.66 vs 0.43) and genuine transactions never exceeding 0.85 meaning any transaction scoring above that threshold is fraud every time in this dataset.

H3: Combining risk score and failed transaction count predicts fraud more accurately than either alone
* Validation: Compare model performance (AUC/precision-recall) using each feature individually vs combined
* Result: Supported
* Summary: The combined model achieved a higher AUC (0.890) than either single feature model (Risk_Score alone: 0.740, Failed_Transaction_Count_7d alone: 0.803), confirming that using both features together captures more information about fraud risk than either does on its own.

H4: Certain transaction types are more commonly associated with fraud
* Validation: Analyse fraud rates by transaction type using a bar chart
* Result: Failed to reject H0 (p = 0.740)
* Summary: Fraud rate is almost identical across all four transaction types suggesting transaction type alone isn't a useful signal for flagging fraud.

H5: Certain locations have a higher incidence of fraud compare to others
* Validation: Analyse fraud rates by location using a bar chart
* Result: Failed to reject H0 (p = 0.624)
* Summary: Fraud rate is almost identical across all five locations suggesting geographic location alone isn't a useful signal for flagging fraud in this dataset.

H6: Fraud is more likely to occur at certain times of the day, on certain days of the week, or on weekends
* Validation: Compare fraud rates by hour of the day using a t-test, by weekend status using a chi-square test, and by day of the week using an ANOVA
* Result: Failed to reject H0 (hour: p = 0.192; weekend vs weekday: p = 0.997; day of week: p = 0.282)
* Summary: Fraud rate doesn't vary by hour of day, weekend status or individual day of the week suggesting time based rules would not be an effective fraud control for this dataset.

## Project Plan

* Business Understanding: Defined the fraud detection objectives and identified the key metrics relevant to the business requirements.
* Data Understanding: Explored the raw dataset, assessed data quality, and identified which features were relevant to the business requirements.
* ETL: Cleaned the raw data, checked for missing values, duplicates, incorrect data types, and outliers, and engineered new features (e.g. hour of day and day of week from the transaction timestamp).
* EDA: Analysed distributions and relationships between features and fraud, and tested six hypotheses using statistical methods (t-tests, chi-square tests, and ANOVA).
* Data Visualisation: Created plots mapped to each hypothesis and business requirement, and built an interactive Tableau dashboard for further exploration.
* Modelling: Built and compared two classification models (Logistic Regression and Random Forest) to predict fraud, using the features identified as significant during EDA.
* Insights & Recommendations: Summarised the findings from the hypothesis testing and the model, and translated them into practical fraud prevention recommendations.

A Kanban board was used to plan and track progress: [insert your GitHub Project board link]

**Project files are organised as followed:**
* (Raw) Primary File: Dataset/Raw/synthetic_fraud_dataset.csv
* (Cleaned) Transformed File: Dataset/CleanData/cleaned_fraud_dataset.csv
* Feature Importance File: Dataset/CleanData/feature_importance.csv
* Model Comparison File: Dataset/CleanData/model_comparison.csv
* Notebooks: jupyter_notebooks/01_ETL.ipynb, 02_EDA.ipynb, 03_Data_Visualisation.ipynb, 04_Modelling.ipynb
* Tableau Dashboard: [insert your published Tableau Public link]

## The rationale to map the business requirements to the Data Visualisations

**Identify which transaction, behavioural and risk-score features are significantly associated with fraud** — box plots of Risk_Score and Failed_Transaction_Count_7d by Fraud_Label plus a supporting bar chart showing fraud rate climbing sharply at 4+ failed transactions.
 
 **Determine whether commonly assumed risk factors actually influence fraud rate** — bar charts of fraud rate by Transaction_Type and Location and charts showing fraud rate by hour, weekend status, and day of week.
 
 **Build and compare classification models** — a feature importance chart from the Random Forest model, and a model comparison chart (AUC) for Logistic Regression vs Random Forest.
 
 **Translate findings into practical recommendations** — the Tableau dashboard pulls the strongest findings together into one interactive view with text callouts summarising each key insight for non-technical readers.
 
 **Present findings for both technical and non-technical audiences** — the notebook plots with statistical test results alongside them serve the technical side, while the Tableau dashboard serves the non-technical side, letting the reader explore the data themselves.
 
 ## Analysis Techniques Used

I used mean, median and standard deviation to compare fraud and genuine transactions across the key numeric variables. To test whether the differences I found were actually significant I ran independent t-tests on the numeric features (H1, H2, and hour for H6) chi-square tests on the categorical ones (H4, H5, and weekend status for H6) and a one-way ANOVA to check for a pattern across the individual days of the week.

I also looked at how all the numeric features correlated with fraud, to get an overall picture before diving into each hypothesis individually.

For the machine learning side I built and compared two classification models Logistic Regression and Random Forest using a scikit-learn pipeline to handle the categorical columns through one-hot encoding.

One thing worth pointing out: several of the hypotheses I expected to matter (transaction type, location, and the time-based ones) turned out not to be statistically significant at all. That was a genuinely useful finding in itself even though it wasn't the result I was expecting going in.

## Ethical Considerations

Since the dataset is fully synthetic and doesn't contain any real personal data, there weren't any actual privacy concerns to deal with here. That said if this kind of analysis were ever applied to real transaction data it would need proper data governance in place such as encryption, limiting who has access and complying with regulations like GDPR.

I also thought about fairness, particularly around location. It would have been easy to assume certain cities are "riskier" for fraud, but my testing actually showed no significant difference in fraud rate across any of the five locations. That's a good reminder not to build fraud rules around assumptions that aren't backed up by the data, since doing so could unfairly single out certain groups or regions without real justification.
## Key Findings

Overall, fraud made up about 32% of the transactions in this dataset — much higher than you'd typically see in real life, but useful for running proper statistical tests.

The two standout predictors were Risk_Score and Failed_Transaction_Count_7d. Both were strongly linked to fraud on their own, and combining them performed even better than either one individually — the combined model reached an AUC of 0.890, compared to just 0.740 for risk score alone and 0.803 for failed transactions alone. Two patterns stood out in particular: any transaction with 4 or more failed attempts in the past 7 days was fraudulent 100% of the time and any transaction with a risk score above 0.85 was fraudulent every single time too.

Everything else I tested  transaction type, location, hour of day, day of week, and weekend status showed no link to fraud at all. That was surprising going in since I expected at least location or time of day to show something.

When it came to modelling Random Forest scored a perfect AUC of 1.00 which sounds great but is actually a red flag rather than a win it likely means the model picked up on how clean and rule based this synthetic dataset is rather than learning something that would hold up on messier, real world data. Logistic Regression with an AUC of 0.89 is the model I'd actually trust more.