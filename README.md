# Predicting Employee Attrition

## Problem Statement
Employee attrition can significantly impact organizational performance and productivity. Predicting when and why employees are likely to leave can help organizations proactively address retention challenges. This README outlines the process and insights gained from building a model to predict employee attrition using the IBM HR Analytics Employee Attrition & Performance dataset.

## Key Steps

1. **Data Collection**: Gathered all necessary data from the IBM HR Analytics Employee Attrition & Performance dataset.
   
2. **Data Preparation**: Cleaned, organized, and standardized data for accuracy.
   
3. **Exploratory Data Analysis (EDA)**:
   - Dropped unnecessary features from the dataset.
   - Compared attrition with categorical and continuous variables, revealing insightful patterns.
   
4. **Insight Generation**: Extracted actionable insights from the analysis:
   - Higher attrition rate among males compared to females.
   - Highest attrition observed among employees aged 28-32.
   - Spikes in attrition at lower income levels, decreasing as income rises.
   - Employees starting their careers with the company tend to leave more than those with longer tenures.
   
5. **Decision Making**: Utilized data-driven strategies to enhance workforce performance and meet organizational goals based on insights generated.

## Steps Achieved

```python
import pandas as pd

# Load the data
data = pd.read_csv('IBM_HR_Analytics.csv')

# Data Cleaning
# Check for null values
if data.isnull().sum().sum() == 0:
    print("Data is clean.")
else:
    print("Null values found, perform data cleaning.")

# Exploratory Data Analysis
# Drop unnecessary features
data.drop(['EmployeeNumber', 'Over18', 'StandardHours', 'EmployeeCount'], axis=1, inplace=True)

# Insights
# Gender disparity
gender_attrition = data.groupby('Gender')['Attrition'].value_counts(normalize=True)

# Age dynamics
age_attrition = data.groupby(pd.cut(data['Age'], bins=[18, 21, 28, 32, 100]))['Attrition'].value_counts(normalize=True)

# Income levels
income_attrition = data.groupby(pd.cut(data['MonthlyIncome'], bins=[0, 5000, 10000, 20000, 1000000]))['Attrition'].value_counts(normalize=True)

# Job satisfaction
job_satisfaction_attrition = data.groupby('JobSatisfaction')['Attrition'].value_counts(normalize=True)

# Departmental differences
dept_attrition = data.groupby('Department')['Attrition'].value_counts(normalize=True)

# Job role impact
job_role_attrition = data.groupby('JobRole')['Attrition'].value_counts(normalize=True)

# Salary increment influence
salary_increment_attrition = data.groupby(pd.cut(data['PercentSalaryHike'], bins=[0, 10, 20, 30, 100]))['Attrition'].value_counts(normalize=True)

# Educational background
education_attrition = data.groupby('Education')['Attrition'].value_counts(normalize=True)

# Salary and stock options
salary_stock_attrition = data.groupby('StockOptionLevel')['Attrition'].value_counts(normalize=True)

# Work-life balance
work_life_attrition = data.groupby('WorkLifeBalance')['Attrition'].value_counts(normalize=True)
