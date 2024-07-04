# Credit Card Financial Dashboard Using Power BI
## Project Objective
To develop a comprehensive credit card weekly dashboard that provides real-time insights into key performance metrics and trends, enabling stakeholders to monitor and analyze credit card operations effectively.
## Dataset Description
1. `credit_card`: No of rows=10,109, No of columns=18. This dataset contains basic information about credit card like Client_Num, Card_Category, Annual_Fees, Activation_30_Days, Customer_Acq_Cost, Week_Start_Date, Week_Num, Qtr, current_year, Credit_Limit, Total_Revolving_Bal, Total_Trans_Amt, Total_Trans_Vol, Avg_Utilization_Ratio, Use Chip, Exp Type, Interest_Earned, Delinquent_Acc. This dataset contains weekly data from January 1, 2023 to 24 December, 2023 (52-weeks data).
2. `customer`: No of rows=10,109, No of columns=15. This dataset contains credit card customers data with columns like Client_Num, Customer_Age, Gender, Dependent_Count, Education_Level, Marital_Status, state_cd, Zipcode, Car_Owner, House_Owner, Personal_loan, contact, Customer_Job, Income, Cust_Satisfaction_Score.
3. `cc_add`: No of rows=186, No of columns=18. This dataset contains same columns as that of 'credit_card' dataset. This dataset contains data after Week 52 i.e., after 24 December, 2023.
4. `cust_add`: No of rows=186, No of columns=15. This dataset contains same columns as that of 'customer' dataset. 
## Preparing Data for Analysis
1. Copying Excel data to PostgreSQL database using SQL queries.
   ### Note: ALL SQL queries are provided in `SQL_Query.sql` file provided above.
2. Connecting PostgreSQL database to Power BI Desktop.
3. 
