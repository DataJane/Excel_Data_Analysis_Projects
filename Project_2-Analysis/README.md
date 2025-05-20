# Project 2: Power Query, Power Pivot & DAX  

# ** UNDER CONSTRUCTION **

## Introduction  
This project explores the job postings data set in further detail and sets out to answer some key questions about the top skills that employers request and how this relates to salary levels.  
Questions Analysed
To understand the dataset, I asked the following questions:

## Table of Contents
- [1. Do more skills result in more pay?](#1do-more-skills-result-in-more-pay)
- [2. What is the salary for data jobs in different regions?](#2-whats-the-salary-for-data-jobs-in-different-regions)
- [3. What are the top skills of data professionals?](#3--what-are-the-top-skills-of-data-professionals)
- [4. What is the pay for the top 10 skills?](#4-whats-the-pay-of-the-top-10-skills)

### Excel Skills Used  
The following skills were utilized for the analysis  
- 🎛️ Pivot Tables
- 📈 Pivot Charts
- 💻 DAX (Data Analysis Expressions)
- ❓ Power Query
- 💪 Power Pivot

### Data Jobs Dataset  
The data used for this project is from Luke Barousse’s Excel course. It contains real-world data from 2023. The dataset contains detailed information on Job titles, Salaries, Locations & Skills.

## 1.	Do more skills result in more pay?  
**Skill: Power Query (ETL)**  
### Extract  
I first used power query to extract the original data (data_salary_all.xlsx) and create two queries:  
- One with the data jobs information
- The second listing all the skills for each job ID 

### Transform
Then I transformed each query by changing column types, removing unnecessary columns, cleaning text to eliminate specific words and characters, and trimming excess whitespace. In addition to splitting and unpivoting the skills data.

Data_jobs_Salary steps  
![Screenshot of applied steps in data_jobs_salary query](https://github.com/user-attachments/assets/b8a6eb1b-7f1f-448f-9113-58a164796490)

Data_jobs_skills steps  
![Screenshot of applied steps in data_jobs_skills query](https://github.com/user-attachments/assets/ceb3a2fd-8b01-430a-9ca0-631bc6523ffd)


### Load
Finally I loaded both transformed queries into the workbook setting the foundation for my subsequent analysis.  

Data_jobs_Salary Power Query view  
![Screenshot of data_jobs_salary query in Power Query](https://github.com/user-attachments/assets/00718a9a-db19-46e9-a5d4-c59e1116aecb)

Data_jobs_skills Power Query view  
![Screenshot of data_jobs_skills query in Power Query](https://github.com/user-attachments/assets/549f37ec-dc38-4362-ab38-e662c6f8e53a)

### Analysis  

I created a scatter plot with a trend line to analyse whether a greater number of skills equates to more pay.
![Scatterplot of skills versus salary with trendline showing an increase in salary with increasing number of skills](https://github.com/user-attachments/assets/7648c361-5140-406a-b620-97815dfe0d79)


### Insights
There is a positive correlation between the number of skills requested in job postings and median salary.  
For example, Business analyst and data analyst require fewer skills than senior data scientist or data scientist and data scientist. There is a corresponding increase in pay.  
Not all increases in skills lead to greater pay. Data Scientist vs Data Engineer and Senior Data Scientist vs Senior Data Engineer require different skill levels but command similar salaries.  

### So What?
Data analysis is a fast evolving field and it is clear that job seekers need to be prepared to continuously learn new skills and keep their skill set up to date.

## 2. What’s the salary for data jobs in different regions?
### Skills: Power Pivot & Dax

### Data Model
I created a data model, integrating the data_jobs_all and data_jobs_skills tables into one model  
Created a one to many relationship between the two queries using job_id in Power Query  

Screenshot of relationship  
![Relationship in the data model between the two queries](https://github.com/user-attachments/assets/77367937-280e-484d-8862-10f29045b34b)

### Analysis
I used the Power Pivot menu to refine the data model & create further measures.  

### DAX
To calculate the the median year salary I used DAX  
```
Median Salary:=MEDIAN(data_jobs_salary[salary_year_avg])   
```
I added a new measure to calculate the median salary filtering for US jobs and non US jobs using the CALCULATE() function  
```
Median Salary Non-US:=CALCULATE([Median Salary],data_jobs_salary[job_country]="United States") 
```
![Screenshot of Power QUery window showing data_jobs_salary query and measures](https://github.com/user-attachments/assets/48130b06-4dcf-4d9e-8592-f004ef90ee71)

### Analysis

I created a Pivot table using the Data Model I created with Power Pivot 
The pivot table and pivot chart show the Job Titles, and median salary (governed by a country slicer), median salary US, and Median Salary Non-US  

### Insights
Senior roles command higher salaries both in the US and internationally showcasing the demand for higher technical skills.  
The disparity between US and non-US salaries is more pronounced in specialist roles e.g. Cloud engineer and Machine Learning Engineer.  

Screenshot of table with slicer showing: Job title median salary US, non US, median salary  
![Screenshot of table with slicer](https://github.com/user-attachments/assets/f1ce03de-2dc3-4c1c-b8a9-8566d4da88e8)

### So What?
This salary information provides useful insights into global markets for data analysts.  

## 3.  What are the top skills of data professionals?
### Skills: Power Pivot & DAX

### Analysis
Skill count is probably not an accurate measure of the likelihood of a skill being requested in a job advertisement, so I created a measure for skill likelihood, as a percentage. 
```
Skill Likelihood:=DIVIDE([Skill Count],[Job Count]) 
```
I created a Pivot table and Bar chart with Job Skills vs Skill Likelihood,  
I added slicers of Job Title and Country, these are linked to all relevant pages to allow further exploration of the data.

![Screenshot of pivot chart showing top skills for Data Analysts](https://github.com/user-attachments/assets/b47f2033-9392-480a-80a7-68999f4bd80e)

### Insights  
What skills dominate: SQL and Python are the most in-demand skills for data professionals.  
For Data Analysts, SQL and Excel are the top two skills.  
This chart shows significant numbers for Emerging technologies like AWS and Azure, highlighting their growing importance to the data professional.  

### So what?
This chart shows the importance of keeping up to date with technology for the data analyst.

## 4. What’s the pay of the top 10 skills?
### Skills: Advanced Charts
### Analysis:
I created a pivot table with Job Skills in the rows and Median Salary in the values. 
However: The filter on the table relationships is one way. As Job Skills is in the rows, I cannot filter on the salary.  
So, I used a CROSSFILTER function within a CALCULATE function to filter on the salary.  
```
Median Salary – Skills:=CALCULATE([Median Salary], CROSSFILTER(data_jobs_salary[job_id],data_jobs_skills[job_id],Both))
```

### Visualisation
I created a Combo chart with Job Skills on the x axis,  
Median Salary – Skills on primary y axis as bars  
Skill Likelihood on secondary y axis, as line with markers, but removed the line and enlarged the markers.  
I made the markers a contrasting colour to assist those with visual challenges.  
I added slicers for: Job Title & Country and connected these to all other sheets, where relevant.  

![Screenshot of Combo chart showing median salary and skill likelihood for each job skill](https://github.com/user-attachments/assets/91d74ce7-1081-4eab-b92b-61635af2e822)


### Insights:
Overall, skills like Spark, AWS & Java command the greatest salaries,  
For data analysis jobs looking at both top pay and likelihood, Python, Tableau and SQL give the greatest returns.  
Word and PowerPoint give the combined lowest returns in this top 10 skills chart.  

### So What?
This chart with it’s added user input gives valuable insight into the top skills required for each data analyst job role. In particular, for data analysts it is worth investing time in learning Python, SQL and Tableau.  

## Conclusion
This detailed analysis gives valuable insights into the essential skills required for data analysis roles. It highlights the importance of continuous learning and staying ahead in an evolving technological landscape. Through this project, I have learned many new techniques that have enhanced my understanding of data analysis. With these newfound insights I am eager to continue my journey, learning more techniques and refining my expertise in data analysis.
