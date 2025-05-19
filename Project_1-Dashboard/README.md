# Project 1: Excel Dashboard
![Screenshot of Dashboard](https://github.com/user-attachments/assets/f109f9e6-5bf7-40b8-8b13-a372e65b61c0)

## Introduction
This data jobs dashboard was designed to investigate salaries for data jobs across different countries. The data is from Luke Barousse’s Excel course, which provides a foundation in analysing data using this powerful tool. The data contains real-world job information from 2023. It contains detailed information on: 
- 👨‍🔧 Job titles,
- 💵 Salaries, 
- 📍 Locations and 
- 💻 Essential skills 

## Dashboard File
My final dashboard is  ![here](https://github.com/DataJane/Excel_Data_Analysis_Projects/blob/main/Project_1-Dashboard/Project%201%20Salary_Dashboard.xlsx)

## Excel Skills Used
The following Excel skills were used in the analysis
- 📈 Charts
- 📐 Formulas and functions
- ✅ Data Validation

## Project Build
### 📈 Charts: 

**Bar Chart: Salary by Job Title**  
![Screenshot 2025-05-18 202717](https://github.com/user-attachments/assets/0bced0f7-ec7b-4088-9b28-212bb8b9bdea)
  
- **Excel Features:** Used bar chart features with formatted salary values and optimised layout for clarity.  
- **Design choice:** Horizontal bar chart for visual comparison of median salaries.  
- **Data organisation:** Sorted by descending salary for ease of readability.  
- **Insights gained:** This enables quick identification of salary trends noting that senior roles and engineers are higher-paying than analyst roles.  
  
  
**Map Chart: Country Median Salaries**  
![Recording of map chart hovering over different countries showing median salaries as tooltips](https://github.com/user-attachments/assets/c193e08f-6164-4dc2-8678-23be87aeac3d)

- **Excel features:** Used the Excel map chart feature to plot salaries globally.  
- **Design Choice:** Map chart allows the user to easily see disparities in salaries across regions.  
- **Data Representation:** Plotted median salary for each region  
- **Insights Gained:** Visually highlights high and low salaried regions for each job title and Country. 

### 📐 Formulas and Functions  
**Calculating Median salary by Country, Job Title and Job Schedule Type**  
```
=MEDIAN(
  IF(
  (jobs[job_title_short]=A2)*
  (jobs[salary_year_avg]<>0)*
  (jobs[job_country]=country)*
  (ISNUMBER(SEARCH(type,jobs[job_schedule_type]))),
  jobs[salary_year_avg]
  )  
)  
```
- **Multi-Criteria Filtering:** The calculations are filtered by job title, country, schedule type and excludes blank salaries.  
- **Array formula:** Uses MEDIAN() function with nested IF() to analyse an array.  
- **Tailored insights:** This enables the dashboard to provide specific salary information tailored for the selected fields.  
- **Formula Purpose:** Formula populates the salary tables, which provides the data for the dashboard charts. An example is given below:   

**Salary by Job Title table**  
![Screenshot of Salary by Job Title table showing a list of job titles with median salary for each one](https://github.com/user-attachments/assets/f6147f5e-7fca-44e0-b6b4-f71d7fcd0e57)

**Salary by Job Title Chart on dashboard**  
![Screenshot of the salary by job title chart on the dashboard](https://github.com/user-attachments/assets/6e397a68-8c0b-4a51-a1b2-f3072db4b2d1)  

### Simplifying Job Schedule Type  

```
=FILTER(J2#,NOT(ISNUMBER(SEARCH("and",J2#)))*(J2#<>0))
```
- **Unique list generation:** This formula utilises the FILTER() function to simplify a complex list of Job Schedule Types, excluding all types that included "and" or were blank. (e.g. Full time and part time)  
- **Formula purpose:** To simplify the input for analysis and the data validation on the dashboard.  
- **Analysis:** The Median salary calculation then uses the SEARCH() function to account for part Job Schedule Types in the analysis.  

**Background Table** (Showing part of the pre-simplified list and the resulting simplified list):   
![Job schedule type table, showing part of the list pre-simplification and the full simplified list of 5 titles.](https://github.com/user-attachments/assets/637dec85-31a4-4753-82f1-6d1b7047a19b)

**Dashboard Implementation:**  
![Job Schedule type chart on the dashboard showing median salaries for each job type (full time, part time, internship etc)](https://github.com/user-attachments/assets/f68f30d0-77e2-486b-9cc7-0b9113c7a24c)


### ✅ Data Validation
Implementing Data Validation rules for entry of Job Title, Country and Type in the Dashboard ensures:  
- Accurate data entry on the dashboard  
- Minimisation of errors  
- Enhanced usability of the dashboard  

![Recording of use of Data Validation for job schedule type input on the dashboard](https://github.com/user-attachments/assets/a23ac9c2-8233-4756-8feb-e57bf001168f)

## **Conclusion**  
I created this dashboard using real-world data on salaries to explore salaries in data related jobs. It highlights my skills in formulas and functions, charts and in data validation. I look forward to solving more problems and learning more data analysis skills.
