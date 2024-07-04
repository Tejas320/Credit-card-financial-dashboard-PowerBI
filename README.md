# Credit Card Financial Dashboard Using Power BI
## Table of Contents
1. [Project Objective](#project_objective)
2. [Dataset Description](#dataset_description)
3. [Preparing Data for Analysis](#preparing_data_for_analysis)
4. [Visualizations](#visualizations)
5. [Project Insights](#project_insights)
## Project Objective
To develop a comprehensive credit card weekly dashboard that provides real-time insights into key performance metrics and trends, enabling stakeholders to monitor and analyze credit card operations effectively.
## Dataset Description
1. `credit_card`: No of rows=10,109, No of columns=18. This dataset contains basic information about credit card like Client_Num, Card_Category, Annual_Fees, Activation_30_Days, Customer_Acq_Cost, Week_Start_Date, Week_Num, Qtr, current_year, Credit_Limit, Total_Revolving_Bal, Total_Trans_Amt, Total_Trans_Vol, Avg_Utilization_Ratio, Use Chip, Exp Type, Interest_Earned, Delinquent_Acc. This dataset contains weekly data from January 1, 2023 to 24 December, 2023 (52-weeks data).
2. `customer`: No of rows=10,109, No of columns=15. This dataset contains credit card customers data with columns like Client_Num, Customer_Age, Gender, Dependent_Count, Education_Level, Marital_Status, state_cd, Zipcode, Car_Owner, House_Owner, Personal_loan, contact, Customer_Job, Income, Cust_Satisfaction_Score.
3. `cc_add`: No of rows=186, No of columns=18. This dataset contains same columns as that of 'credit_card' dataset. This dataset contains data after Week 52 i.e., after 24 December, 2023.
4. `cust_add`: No of rows=186, No of columns=15. This dataset contains same columns as that of 'customer' dataset. 
## Preparing Data for Analysis
1. Copying Excel data to PostgreSQL database using SQL queries.
   ### Note: ALL SQL queries are provided in `SQL-Query.sql` file provided above.
2. Connecting PostgreSQL database to Power BI Desktop and importing the dataset.
3. Creating a new column 'Revenue' in 'credit_card' dataset.
   ```bash
   Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]
   ```
4. Created a new column 'week_num2' in 'credit_card' dataset.
   ```bash
   week_num2 = WEEKNUM('public cc_detail'[week_start_date])
   ```
5. Created a new measure 'Current_week_revenue' in 'credit_card' dataset.
   ```bash
   Current_week_revenue = CALCULATE(SUM('public cc_detail'[Revenue]), FILTER(ALL('public cc_detail'), 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])))
   ```
6. Created a new measure 'Previous_week_revenue' in 'credit_card' dataset.
   ```bash
   Previous_week_revenue = CALCULATE(SUM('public cc_detail'[Revenue]), FILTER(ALL('public cc_detail'), 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1))
   ```
7. Created a new measure 'WOW_revenue' in 'credit_card' dataset.
   ```bash
   WOW_revenue = DIVIDE(([Current_week_revenue] - [Previous_week_revenue]), [Previous_week_revenue])
   ```
8. Created a new column 'AgeGroup' in 'customer' dataset.
   ```bash
   AgeGroup = SWITCH(TRUE(), 'public cust_detail'[customer_age] < 30, "20-30", 'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40", 'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50", 'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60", 'public cust_detail'[customer_age] >= 60, "60+", "unknown")
   ```
9. Created a new column 'IncomeGroup' in 'customer' dataset.
   ```bash
   IncomeGroup = SWITCH(TRUE(), 'public cust_detail'[income] < 35000, "Low", 'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] < 70000, "Medium", 'public cust_detail'[income] >= 70000, "High", "unknown")
   ```
## Visualizations
Two Power BI reports are made - Credit Card Transaction Report, Credit Card Customer Report.
## Credit Card Transaction Report
1. Created a Table visualizing Sum of Revenue, Sum of total_trans_amt and Sum of interest_earned according to credit card category.
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/b43904f4-f0aa-42d5-85bc-8e19a22b9c1a)
2. Created a Line and Stacked Column Chart visualizing Quarterly Revenue and Total Transaction Count.
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/537765c3-9fef-47bc-9d8d-4754e18d4ac5)
3. Created a Stacked bar chart visualizing Revenue by Expenditure Type.
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/0b179889-f8c6-4920-9526-828c9b797f56)
4. Created a Stacked bar chart visualizing Revenue by Customer Job.
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/c59b57c0-0d49-4e6c-bb18-b3acbfdaa847)
5. Created a Stacked bar chart visualizing Revenue by Education Level
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/d1d64a51-ccef-4b56-bab1-ca7e8e7c6b9b)
6. Created a Stacked bar chart visualizing Revenue by Use Chip.
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/7e18dde4-98a4-4b0e-890c-e84aba0a5f24)
7. Created a Stacked bar chart visualizing Customer Acquisition Cost according to credit card category.
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/7e1dedd5-9fcc-4bc0-9a52-bf18f4528fae)
8. Created multiple cards for visulaizing Total Revenue, Total Interest, Total Amount and Total Transaction Count.
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/4b02a7a2-466b-440f-8f46-36c7ca48dc3a)
9. Created multiple slicers of gender, credit card category, quarters, income group and week start date.
    ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/3cbbfb6c-b765-4bb1-98fb-b1e93af4b2d0)
    ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/0cb500bc-f02f-41da-976c-a26797e391de)
### Final Credit Card Transaction Report Dashboard
![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/bcb8f178-8dd3-4014-8b1d-42fa8afc24d7)
## Credit Card Customer Report
1. Created a Treemap visualizing gender with their total revenue count depicting color codes for each gender to be used throughout this report.
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/d162e5fb-d5ae-4664-b87b-366bc256729c)
2. Created a Line chart visualizing total revenue by week gender wise.
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/c5f6f6d7-7cb4-41b7-9095-8cbd7866ca4e)
3. Created a Table visualizing Sum of Revenue, Sum of interest_earned and Sum of income according to customer job.
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/1ce10225-f224-4201-acdf-142fd2a0a570)
4. Created a Stacked bar chart visualizing Revenue by Age Group gender wise.
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/45ea6c0c-bb16-408c-8389-e1b9bcf9ad7a)
5. Created a Stacked bar chart visualizing Top 5 States according to highest revenue of customers gender wise.
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/b5efae5b-ee2d-445e-97d0-915ae1bb13fc)
6. Created a Stacked bar chart visualizing Revenue by Marital Status of customer gender wise.
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/75102df5-8f3c-4873-9b28-f8ff844de0e0)
7. Created a Stacked bar chart visualizing Revenue by Income Group of customers gender wise.
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/db6c6d05-1bda-4384-ae3c-f59b917c2e57)
8. Created a Stacked bar chart visualizing Revenue by Dependent Count of customers gender wise.
   ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/301629a2-220a-4ea9-94d5-6c7ff950e7de)
9. Created a Stacked bar chart visualizing Revenue by Education Level of customers gender wise.
    ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/962ffa58-377b-403a-9cb8-8b2b48253af6)
10. Created multiple cards for visualizing Total Revenue, Total Interest, Total Income and Customer Satisfaction Score (CSS).
    ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/660112ca-e079-43cd-ab2e-b1266e732921)
11. Created multiple slicers of use chip, credit card category, quarters and week start date.
    ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/342d5f85-7ff6-4492-a39a-7b2cc8203cfb)
    ![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/4805716b-e2c2-4d5f-8ced-22d0fa48df3f)
### Final Credit Card Customer Report Dashboard
![image](https://github.com/Tejas320/Credit-card-financial-dashboard-PowerBI/assets/73283098/f625ddf8-f355-463f-84d6-0e7707509778)
## Project Insights
### WOW (Week On Week) change:
- Revenue increased by 28.8%
- Total transaction amount and count increased by % and %
- Customer count increased by %
### Overview YTD:
- Overall revenue is 57M
- Total interest is 8M
- Total transaction amount is 46M
- Male customers are contributing more in revenue 31M, females 26M
- Blue and silver credit cards are contributing to 93% of overall transactions
- TX, NY and CA are contributing to 68%
- Overall activation rate is 57.5%
- Overall delinquent rate is 6.06%






