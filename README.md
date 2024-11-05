# HR Employee Retention and Attrition Analysis

## Table of Contents
- [Project Overview](#project-overview)


- [Project Objectives](#project-objectives)


- [Key Metrics](#key-metrics)


- [Data Sources](#data-sources)


- [Data Collected](#data-collected)


- [Tools Used](#tools-used)


- [Data Cleaning and Preparation](#data-cleaning-and-preparation)


- [Data Analysis](#data-analysis)


- [Data Visualization](#data-visualization)


- [Visual Analysis](#visual-analysis)


- [Summary of HR Data Analysis](#summary-of-hr-data-analysis)


- [Recommendations](#recommendations)




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
```
Attrition Rate = SUM('HR data'[Attrition Count])/SUM('HR data'[Employee Count])

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
```


### Data Visualization 
---
![Overview HR Attrition](https://github.com/user-attachments/assets/a5c6f705-05df-4bb5-b9ca-afd4d4fad56b)
![Demographics 1](https://github.com/user-attachments/assets/029b4177-c141-4230-8da9-d6d9bed2f68b)
![Demographics 11](https://github.com/user-attachments/assets/a4fd15bd-fb8a-47f4-911e-06e8d9233cc5)
![Employee turnover](https://github.com/user-attachments/assets/38f9cca6-a399-42ad-be2b-b2848afbff13)
![Retention Strategies](https://github.com/user-attachments/assets/e3bd3e52-4777-419b-ab5f-18c9acd78688)
![Employee Satisfaction](https://github.com/user-attachments/assets/edbbbbfa-2757-4c5b-8900-1d13e8de4d04)

### Visual Analysis
---
#### Overview of HR Data Analysis Tracker
- This section provides a high-level summary of the key metrics, including demographics, employee turnover, retention strategies, and employee satisfaction.
- Key Metrics: Total employees, attrition rate, gender distribution, and average tenure.
- Implications: These metrics set the foundation for understanding the scale of attrition and areas where retention strategies might be focused.

### 1. Demographics 1
###### Employees by Age Band and Gender: Under 25: 41 (Male: 20, Female: 21), 25-34: 268 (Male: 86, Female: 182), 35-44: 272 (Male: 90, Female: 182), 45-54: 186 (Male: 136, Female: 50), Over 55: 46 (Male: 32, Female: 14)
- Insight: The largest age groups are 25-34 and 35-44, with females representing a higher proportion in these age ranges. Employees over 45 are predominantly male, indicating that gender balance may shift with age.
- Recommendation: Consider implementing targeted retention initiatives focusing on the largest demographics, such as career development for employees aged 25-44 and flexible benefits for those over 45.

###### Employees by Marital Status and Gender: Married: 348 (Female: 152, Male: 186), Single: 479 (Female: 152, Male: 198), Divorced: 96 (Female: 87, Male: 9)
- Insight: Most employees are single (around 38.8%), with females making up a large proportion of the divorced category. This suggests that marital status could influence benefit preferences.
- Recommendation: Consider offering flexible or customizable benefits that accommodate varied needs based on marital status.

###### Attrition by Gender: Higher Attrition: Male: 150 (63.29%), Female: 87 (36.71%)
- Insight: Male employees have a higher attrition rate, making up about 63.29% of total attrition. This may highlight certain workplace challenges more specific to male employees.
- Recommendation: Conduct further analysis to understand and address factors contributing to higher male attrition, potentially through tailored engagement programs.

###### Attrition by Educational Field: Life Sciences: 89 (37.6%), Medical: 63, Marketing: 35, Technical Degree: 32, Other: 11, Human Resources: 7
- Insight: Life Sciences and Medical fields have the highest attrition counts, with Life Sciences making up over one-third of total attrition.
- Recommendation: Explore job conditions, career growth, or other specific challenges in these fields to improve retention.

###### Attrition Count by Distance Category: Far: 60 (25.32%), Near: 94 (39.66%), Very Far: 83 (35.02%)
- Insight: Employees living "Very Far" from work have a significant attrition rate (35.02%), though those living "Near" also show notable attrition (39.66%).
- Recommendation: Offer remote work or flexible hours to retain employees with challenging commutes.

### 2. Demographics II Visual Analysis (Attrition by Age Group and Gender)

###### Attrition by Age: Under 30: 22% attrition rate, 30-40: 15% attrition rate, Over 40: 10% attrition rate while gender-based attrition consist of Male: 14%, Female: 18%
- Analysis: Younger employees (under 30) experience the highest attrition rate at 22%, indicating that career progression or job satisfaction might be areas of concern.
Also, female employees have a higher attrition rate (18%) compared to male employees (14%), suggesting a need to investigate and address gender-specific retention challenges.
- Implications: Consider targeted programs such as mentorship for younger employees and initiatives focused on supporting women in the workplace.

### 3. Employee Turnover Visual Analysis

###### Attrition Count by Tenure: Newcomer (1-5 years): 162 employees, Experienced (6-15 years): 62 employees, Veteran (16-40 years): 13 employees
- Insight: The majority of turnover (68.4%) is among employees with 1-5 years of tenure, suggesting that new hires may face challenges in adjusting or finding growth opportunities.
- Recommendation: Implement onboarding support and early-career development programs to engage and retain newer employees.

###### Job Satisfaction by Job Role: Sales Executive: 34 employees "Very Dissatisfied," 16 "Dissatisfied", Research Scientist: 13 employees "Very Satisfied", Sales Representative: 16 employees "Very Dissatisfied," 14 "Dissatisfied"
- Insight: Sales Executives and Sales Representatives show high dissatisfaction, which might indicate job-specific challenges in these roles. Research Scientists, however, show higher satisfaction, particularly in the "Very Satisfied" category.
- Recommendation: Review working conditions, targets, and incentives for Sales roles to address dissatisfaction and improve job satisfaction.

###### Attrition Count by Job Involvement: Very Low: 28 employees, Low: 71 employees, Good: 125 employees and Very Good: 13 employees
- Insight: Employees with "Good" job involvement have the highest attrition (125), which might indicate that involvement alone does not prevent turnover.
- Recommendation: Assess other retention factors beyond job involvement, such as career progression and work-life balance, for employees with "Good" involvement.

###### Attrition Count by Department: HR: 56.12% of attrition, Sales: 38.82% of attrition and R&D: 5.06% of attrition
- Insight: HR and Sales departments experience the highest attrition, with HR alone contributing to over half of the total attrition (56.12%).
- Recommendation: Conduct targeted assessments within HR and Sales to understand specific turnover drivers and implement department-specific retention strategies.

###### Attrition Count Over Time: Yes (Attrition occurred): 110 employees and No (No attrition): 127 employees
- Insight: This shows a relatively balanced distribution between employees who stayed and those who left, suggesting turnover is ongoing and consistent.
- Recommendation: Track attrition patterns over time to identify any specific periods with higher attrition and address possible seasonal or cyclical turnover trends.

###### Job Satisfaction by Educational Field: Human Resources - 66 employees "Very Dissatisfied," 46 "Dissatisfied", Life Sciences: 29 employees "Very Satisfied," 18 "Satisfied", Marketing: Higher dissatisfaction with 4 "Very Dissatisfied" and 11 "Dissatisfied".
- Insight: Employees in HR show the most dissatisfaction, with high counts in "Very Dissatisfied" and "Dissatisfied" categories. Conversely, employees in Life Sciences have higher satisfaction levels, particularly in the "Very Satisfied" group.
- Recommendation: Address specific satisfaction issues within HR, potentially through training, support programs, or improved career paths to enhance employee experience in that educational field.

### 4. HR Retention Strategies Visual Analysis
Total Employees: 1,470, Attrition Count: 237, Attrition Rate: 16%, Average Salary: $6.5K, Average Salary Hike: 15.21%
The attrition rate of 16% shows room for improvement in retention. The average salary hike of 15.21% is competitive but may need adjustment in some areas.

###### Income Category: Less than 10k: 272 employees, 10k - 15k: 20 employees, Above 15k: 5 employees
- Insight: Lower-paid employees are leaving at higher rates. 
- Recommendation: Reassess compensation for those earning under 10k to improve retention.

###### Stock Options: Very Poor: 154 employees, Poor: 56 employees, Medium: 12 employees, High: 15 employees
- Insight: Employees with "Very Poor" or "Poor" stock options are more likely to leave.
- Recommendation: Enhance stock option offerings for these groups to increase retention.

###### Training: 0 Trainings: 38 employees, 1 Training: 69 employees, 2 Trainings: 50 employees, 3+ Trainings: 80 employees
- Insight: Employees with fewer training sessions have higher attrition.
- Recommendation: Provide more training opportunities to encourage growth and reduce turnover.

###### Promotion Category: 0-5 Years: 202 employees, 6-10 Years: 27 employees, 11-15 Years: 8 employees
- Insight: Attrition is highest among employees with 0-5 years of tenure, likely due to limited promotion opportunities.
- Recommendation: Offer clearer promotion paths and mentorship for newer employees.

###### Salary Hike Category: Low: 150 employees, Medium: 57 employees, High: 30 employees
- Insight: Employees with "Low" salary hikes are leaving at higher rates.
- Recommendation: Ensure fair salary hikes, especially for high-performing employees in the "Low" category.

### 5. Employee Satisfaction Visual Analysis 

- Overall Metrics: Current Employees: 1,233, Current Female Employees: 501, Current Male Employees: 732 Attrition Rate: 16%, Attrition Count: 237
These metrics set the foundation for analyzing satisfaction and its impact on attrition.

###### Attrition Count by Relationship Status: Very Dissatisfied: 57 employees, Dissatisfied: 45 employees, Satisfied: 71 employees, Very Satisfied: 64 employees

- Insight: Attrition is highest among "Satisfied" employees (71), followed closely by "Very Satisfied" employees (64). This may suggest that relationship satisfaction alone doesn’t significantly prevent turnover.
- Recommendation: Investigate other factors beyond relationship satisfaction that may influence attrition, even for satisfied employees.
  
###### Attrition Count by Performance Rating: Satisfactory: 200 employees (84.39%), Outstanding: 37 employees (15.61%)

- Insight: A majority of employees leaving (84.39%) have a "Satisfactory" rating, while fewer (15.61%) with "Outstanding" ratings are leaving.
- Recommendation: Recognize and motivate employees with "Satisfactory" ratings through development programs to improve retention.

###### Attrition Count by Job Satisfaction Status: Very Dissatisfied: 66 employees, Dissatisfied: 46 employees, Satisfied: 73 employees, Very Satisfied: 52 employees

- Insight: Attrition is highest among employees with a "Satisfied" status (73), which suggests that "Satisfaction" alone does not ensure retention.
- Recommendation: Identify additional ways to increase job satisfaction, especially for those currently "Satisfied."

###### Attrition Count by Environment Status: Very Dissatisfied: 72 employees, Dissatisfied: 43 employees Satisfied: 62 employees, Very Satisfied: 60 employees.
- Insight: The highest attrition count is among those who are "Very Dissatisfied" (72). This indicates that environmental dissatisfaction strongly correlates with turnover.
- Recommendation: Improve the work environment, particularly for those expressing dissatisfaction, to lower attrition rates.

###### Attrition Count by Business Travel: Non-Travel: 156 employees, Travel Rarely: 69 employees, Travel Frequently: 12 employees
- Insight: Employees who do not travel show a significantly higher attrition count (156), suggesting that a lack of travel could be associated with higher turnover.
- Recommendation: Assess the reasons why non-traveling employees might be leaving, perhaps by offering flexible or diverse work opportunities.

###### Attrition Count by Work-Life Balance: Poor: 25 employees, Fair: 58 employees, Good: 127 employees, Excellent: 27 employees
- Insight: Attrition is highest among employees with "Good" work-life balance (127). This may indicate that the perceived level of work-life balance is not the main issue affecting turnover.
- Recommendation: Look into other aspects of employee experience for those with "Good" work-life balance to understand the underlying reasons for their departure.

### Summary of HR Data Analysis
---
This analysis highlights key areas in employee demographics, turnover, retention, and satisfaction.

##### Key Insights:
- Demographics: The 25-44 age group has a higher number of females, while employees 45+ are mostly male. Most employees are single (39%), and divorced employees are predominantly female. High attrition is seen in Life Sciences and Medical fields and among employees with long or short commutes.
- Turnover: Male employees have a higher turnover rate (63%). Life Sciences and Medical fields show significant turnover, indicating job satisfaction issues.
- Retention Strategies: Career development for the 25-44 age group and flexible benefits based on marital status could improve retention. Remote work options may also help reduce turnover for employees with difficult commutes.
- Satisfaction: Satisfaction varies across groups, indicating a need for tailored improvements in engagement, benefits, and career opportunities.
  
### Recommendations
---
- Retention Programs: In terms of age-focused development, there should be career growth programs for the 25-44 age range and provision of benefits tailored to marital status (single, married, divorced).
- Gender-Specific Engagement: Address high male attrition with targeted engagement and support programs.
- Field-Specific Support: Investigate high turnover in Life Sciences and Medical fields to address any specific challenges.
- Flexible Work Options: Offer remote work or flexible hours to employees with challenging commutes.
- Feedback Mechanisms: Regularly collect feedback to keep up with employee needs and improve retention strategies.

