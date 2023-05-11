# HR DASHBOARD WITH POWERBI


# OVERALL LAYOUT
![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/48c8b9a2-3dcb-4200-a27e-425785c83433)
![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/7786abd0-f9b6-43f3-b3d0-71f8834c470d)
![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/f13309c6-8c8a-4581-adae-7176e418c06d)

# Datasets
2 csv files:
- HR Analytics Data
  + Columns: Age, Attrition, BusinessTravel, DailyRate, Department, DistanceFromHome, Education, EducationField, EmployeeCount, EmployeeNumber, EnvironmentSatisfaction, Gender, HourlyRate, JobInvolvement, JobLevel, JobRole, JobSatisfaction, MaritalStatus, MonthlyIncome, MonthlyRate, NumCompaniesWorked, Over18, OverTime, PercentSalaryHike, PerformanceRating, RelationshipSatisfaction, StandardHours, StockOptionLevel, TotalWorkingYears, TrainingTimesLastYear, WorkLifeBalance, YearsAtCompany, YearsInCurrentRole, YearsSinceLastPromotion, YearsWithCurrManager

- HR Employee Data
  + Columns: EmployeeNumber,	Emplyee name

# Data Tranformation with Power Query Editor
## Data Preprocessing
![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/c2386391-4aa7-4071-9f36-d6530c90dafb)

## Merged two files on "EmployeeNumber"
![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/1488cf2d-43f2-4fab-b1e3-6fa8ab238cf2)

# Data Visualization
## "Home" Page
### 1. Overview of Total Employees and Gender Diversity

Create new measures using DAX
- "Total Employee":  Total Employee = COUNTROWS('HR Analytics Data')
- "Male": Male = CALCULATE([Total Employee],'HR Analytics Data'[Gender] = "male" )
- "% Male": % Male = DIVIDE('All Measures'[Male],[Total Employee],0)
- "Female": Female = CALCULATE([Total Employee],'HR Analytics Data'[Gender] = "female" )
- "% Female": % Female = DIVIDE('All Measures'[Female],[Total Employee],0)

Result: ![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/d4b19506-9448-45fb-8412-17b6958066e5)

### 2. Find who had never been promoted since the last 10 years and above is now due for promotion.

Add Conditional Column: "Promotion Status" based on "YearsSinceLastPromotion" column
![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/d50d652b-2c04-4b5e-9040-cbcca5513125)
Create new measures using DAX:
- "Due for promotion": Due for promotion = CALCULATE([Total Employee],'HR Analytics Data'[Promotion Status]="Due for promotion")
- "% Due for promotion": % Due for promotion = DIVIDE([Due for promotion],[Total Employee],0)
- "Not Due": Not Due = CALCULATE([Total Employee],'HR Analytics Data'[Promotion Status]="Not Due")
- "% Not Due": % Not Due = DIVIDE([Not Due],[Total Employee],0)

Result: ![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/31fe7548-002d-459b-9928-34ada229fc44)

### 3. Find out how many employees who have worked for more than 10 years to be retrenched.

Add Conditional Column: "Retrenchement Status" based on "YearsAtCompany" column
![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/2bf8434a-2c34-4b14-a24b-a47104824ba1)

Create new measures using DAX:

- "On Working": On Working  = IF(ISBLANK(CALCULATE([Total Employee],'HR Analytics Data'[Retrenchment Status] = "On Working")),0,CALCULATE([Total Employee],'HR Analytics Data'[Retrenchment Status] = "On Working"))
- "% On working": % On working = DIVIDE([On Working],[Total Employee],0)
- "Will be retrenched": Will be retrenched = IF(ISBLANK(CALCULATE([Total Employee],'HR Analytics Data'[Retrenchment Status] = "Will be retrenched")),0,CALCULATE([Total Employee],'HR Analytics Data'[Retrenchment Status] = "Will be retrenched"))
- "% Will be retrenched": % Will be retrenched = DIVIDE([Will be retrenched],[Total Employee],0)

Result: ![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/5e7471bf-f454-4e6a-833d-e044691226fc)

### 4. Find out how many workers live very far, near, close to the office.

Add Conditional Column: "Distance Status" based on "DistanceFromHome" column
![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/21c2df3c-5feb-4d16-8e7b-a566cc57ccc8)

Result: ![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/11252e16-0b17-4026-9e5b-78f3b71400f4)

## "Details" Page

### 1. Find out the level of job satisfaction among employees
Add Conditional Column: "Job Satisfaction Level" based on "JobSatisfaction" column
![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/f5959a62-d8a2-45bf-b46b-700884bd7f2a)

Result: ![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/0ae2e981-5516-413d-9259-228ce098cfcf)

### 2. Find out the Performance Rating of employee

Add Conditional Column: "Performance Rating" based on "PerformanceRating" column
![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/05d1d775-ddb8-4262-81cf-cac198af667e)

Create new measures using DAX:
- "High Rated": High Rated = CALCULATE([Total Employee],'HR Analytics Data'[Performance Rating]="High Rating")
- "% High rated": % High rated = DIVIDE([High Rated],[Total Employee])
- "Low Rated": Low Rated = CALCULATE([Total Employee],'HR Analytics Data'[Performance Rating]="Low Rating")
- "% Low rated": % Low rated = DIVIDE([Low Rated],[Total Employee])

Result: ![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/ed5ea706-e30d-42e9-b77e-19b82dc5bab9)

## "Demographics" Page
### Age and Gender Diversity

Add Conditional Column: "Age Bins" based on "Age" column
![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/81baeb4a-3436-49c3-9e9c-cd6f9f104868)

Result: ![image](https://github.com/nnanhvan/HR_Dashboard_PowerBI/assets/115717767/ddb2918e-02be-445d-bf1f-ee945d5a565b)


