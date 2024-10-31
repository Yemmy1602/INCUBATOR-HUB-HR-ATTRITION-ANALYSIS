# Employee Retention and Attrition Analysis
### Project Overview
---
In this project, the main focus is to analyze and understand employee attrition—why employees are leaving the company—and to identify areas where improvements can be made to retain staff. The analysis will look at several critical factors that may influence an employee's decision to stay or leave, using Power BI to visualize trends and insights

### Project Objectives
---
This project was designed to address the following analysis:

- Identify Key Attrition Factors: Investigate what causes employee attrition, focusing on factors like Department, Job role, Job satisfaction, Tenure, and Demographics (Age, Gender), that may need targeted retention efforts.
- Analyze Employee Satisfaction and Tenure: Measure satisfaction levels by department, role, and tenure to see how they relate to attrition.
- Evaluate Impact of Retention Strategies: Assess the effectiveness of retention initiatives like Work-life Balance Programs, Promotion, Increment in Salary, Access to Stock options, Rewards, Professional Development, and Career Growth.

### Key Metrics
---
- Attrition Rate: Percentage of employees leaving over a specific period.
- Satisfaction Levels: Average job satisfaction scores by department, role, and demographic.
- Tenure: Average length of service by demographic and department.
- Turnover by Performance: Relationship between performance ratings and attrition rates.

### Data Sources
---
This Data primary source used is HR attrition and retention.csv from Capstone

### Data Collected
---
Here is an overview of the columns in the HR dataset along with their descriptions: 
1. Employee Number: A unique identifier for each employee in the dataset. 
2. MonthlyIncome: The monthly income of the employee. 
4. Num Companies Worked: The number of companies the employee has worked for before joining the 
current organization. 
5. Over18: Indicates whether the employee is over 18 years old (Yes/No). 
6. OverTime: Indicates whether the employee is working overtime (Yes/No). 
7. Percent Salary Hike: The percentage increase in the employee's salary during their time at the 
organization. 
8. Performance Rating: The performance rating given to the employee, typically on a scale (e.g., 3-4). 
9. Relationship Satisfaction: The employee’s satisfaction with their relationships at work, often on a scale 
(e.g., 1-4). 
11. Stock Option Level: The level of stock options granted to the employee, typically on a scale (e.g., 0-3). 
12. Total Working Years: The total number of years the employee has worked across all organizations. 
13. Training Times Last Year: The number of times the employee received training in the last year. 
14. Work Life Balance: The employee’s rating of their work-life balance, typically on a scale (e.g., 1-4). 
15. Years At Company: The number of years the employee has been with the current organization. 
16. Years In Current Role: The number of years the employee has been in their current role within the organization. 
17. Years Since Last Promotion: The number of years since the employee’s last promotion. 
18. Years With Curr Manager: The number of years the employee has been working with their current 
manager. 
19. Age: The age of the employee. 
20. Attrition: Indicates whether the employee has left the organization (Yes/No). 
21. BusinessTravel: The frequency of business travel required by the employee (e.g., "Travel_Rarely", "Travel_Frequently", "Non-Travel"). 
23. Department: The department in which the employee works (e.g., "Sales", "Research & Development", "Human Resources"). 
24. Distance From Home: The distance between the employee's home and their workplace. 
25. Education: The education level of the employee, typically on a scale (e.g., 1-5). 
26. Education Field: The field of education of the employee (e.g., "Life Sciences", "Medical", 
"Marketing"). 
27. Environment Satisfaction: The employee’s satisfaction with the working environment, typically on a scale (e.g., 1-4). 
28. Gender: The gender of the employee (e.g., Male, Female). 
30. Job Involvement: The level of the employee’s involvement in their job, typically on a scale (e.g., 1-4). 
31. Job Level: The job level of the employee within the organization, typically on a scale (e.g.,
1-5). 
33. Job Role: The specific role or position of the employee within the organization (e.g., "Sales 
Executive", "Research Scientist"). 
34. Job Satisfaction: The employee’s satisfaction with their job, typically on a scale (e.g.,1-4). 
35. Marital Status: The marital status of the employee (e.g., "Single", "Married", "Divorced").

### Tools Used
---
- Microsoft Excel
- Power BI: For data visualization and reporting.
- DAX: Used to create custom metrics and calculations.

### Data Cleaning and Preparation
---
- Data Loading and Inspection
- No Missing Variables
- No Data Cleaning and Formatting
- Creation of Calculated columns and measures

### Data Analysis
---
The following are the DAX Expressions used during my Analysis

```Attrition Rate = SUM('HR data'[Attrition Count])/SUM('HR data'[Employee Count])

AverageSalary = [Monthly Salary]/[EmployeeCount]

AvgAge = AVERAGE('HR data'[Age])/AVERAGE('HR data'[Employee Count])

AvgSalaryHike = AVERAGE('HR data'[Percent Salary Hike])

EmployeeCount = DISTINCTCOUNT('HR data'[Employee Number])

Monthly Salary = SUM('HR data'[Monthly Income])

EnvironmentStatus = SWITCH(TRUE(), 
HR data'[Environment Satisfaction] = 1, "Very Dissatisfied", 
'HR data'[Environment Satisfaction] = 2, "Dissatisfied", 
'HR data'[Environment Satisfaction] = 3, "Satisfied", 
'HR data'[Environment Satisfaction] = 4, "Very Satisfied")

Income Category = 
SWITCH(
    TRUE(), 
    'HR data'[Monthly Income] < 10000, "Less than 10k",
    'HR data'[Monthly Income] >= 10000 && 'HR data'[Monthly Income] < 15000, "Btw 10k - 15k",
    'HR data'[Monthly Income] >= 15000, "Above 15k")
    
Job_involvement = SWITCH(TRUE(), 
'HR data'[Job Involvement] = 1, "Very Low", 
'HR data'[Job Involvement] = 2, "Low", 
'HR data'[Job Involvement] = 3, "Good", 
'HR data'[Job Involvement] = 4, "Very Good")

Performance Status = SWITCH(TRUE(), 
'HR data'[Performance Rating] = 3, "Satisfactory", 
'HR data'[Performance Rating] = 4, "Outstanding")

PromotionCategory = 
SWITCH(
    TRUE(),
    'HR data'[Years Since Last Promotion] >= 0 && 'HR data'[Years Since Last Promotion] <= 5, "0-5years",
    'HR data'[Years Since Last Promotion] >= 6 && 'HR data'[Years Since Last Promotion] <= 10, "6-10years",
    'HR data'[Years Since Last Promotion] >= 11 && 'HR data'[Years Since Last Promotion] <= 15, "11-15years",
    'HR data'[Years Since Last Promotion] > 15, "Above 15years"
)

RelationshipStatus = SWITCH(TRUE(), 
'HR data'[Relationship Satisfaction] = 1, "Very Dissatisfied", 
'HR data'[Relationship Satisfaction] = 2, "Dissatisfied", 
'HR data'[Relationship Satisfaction] = 3, "Satisfied", 
'HR data'[Relationship Satisfaction] = 4, "Very Satisfied")

SalaryHikeCategory = 
SWITCH(
    TRUE(),
    'HR data'[Percent Salary Hike] >= 11 && 'HR data'[Percent Salary Hike] <= 15, "Low",
    'HR data'[Percent Salary Hike] >= 16 && 'HR data'[Percent Salary Hike] <= 20, "Medium",
    'HR data'[Percent Salary Hike] >= 21 && 'HR data'[Percent Salary Hike] <= 25, "High")

StockOptionCategory = SWITCH(TRUE(), 
'HR data'[Stock Option Level] = 0, "Very Poor", 
'HR data'[Stock Option Level] = 1, "Poor", 
'HR data'[Stock Option Level] = 2, "Medium", 
'HR data'[Stock Option Level] = 3, "High")

Tenure = SWITCH(TRUE(), 
'HR data'[Years At Company] >= 0 && 'HR data'[Years At Company] <= 5, "Newcomer (1-5)",
'HR data'[Years At Company] >= 6 && 'HR data'[Years At Company] <= 15, "Experienced (6-15)", 
'HR data'[Years At Company] >=16 && 'HR data'[Years At Company] <= 40, "Veteran (16-40)")
