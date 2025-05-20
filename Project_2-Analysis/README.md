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

1.	Do more skills result in more pay?
2.	What is the salary for data jobs in different regions?
3.	What are the top skills of data professionals?
4.	What is the pay for the top 10 skills?  

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

Data_jobs_all steps  
Data_jobs_skills steps  

### Load
Finally I loaded both transformed queries into the workbook setting the foundation for my subsequent analysis.  

Data_jobs_all PQ view  
Data_jobs_skills PQ view  

### Analysis  

I created a scatter plot with a trend line to analyse whether a greater number of skills equates to more pay.

Screenshot: Graph  

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
Created a one to many relationship between the two tables using job_id in Power Query  

Screenshot of relationship  

### Analysis
I used the Power Pivot menu to refine the data model & create further measures.  
I created a Pivot table using the Data Model I created with Power Pivot  
Analysing with job_title_short in the rows area and salary_year_avg in the values area  

### DAX
To calculate the the median year salary I used DAX  
```
Median Salary:=MEDIAN(data_jobs_salary[salary_year_avg])   
```
I added a new measure to calculate the median salary filtering for US jobs and non US jobs using the CALCULATE() function  
```
Median Salary Non-US:=CALCULATE([Median Salary],data_jobs_salary[job_country]="United States") 
```

### Analysis
I created a pivot table and pivot chart showing the Job Titles, and median salary (governed by a country slicer), median salary US, and Median Salary Non-US  

### Insights
Senior roles command higher salaries both in the US and internationally showcasing the demand for higher technical skills.  
The disparity between US and non-US salaries is more pronounced in specialist roles e.g. Cloud engineer and Machine Learning Engineer.  

Screenshot of table with slicer  

Job title median salary US, non US, median salary  

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
Insights  
What skills dominate: SQL and Python are the most in-demand skills for data professionals.  
For Data Analysts, SQL and Excel are the top two skills.  
Emerging technologies like AWS and Azure show significant numbers on the chart, highlighting their growing importance to the data professional.  

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

### Insights:
Overall, skills like Spark, AWS & Java command the greatest salaries,  
For data analysis jobs looking at both top pay and likelihood, Python, Tableau and SQL give the greatest returns.  
Word and PowerPoint give the combined lowest returns in this top 10 skills chart.  

### So What?
This chart with it’s added user input gives valuable insight into the top skills required for each data analyst job role. In particular, for data analysts it is worth investing time in learning Python, SQL and Tableau.  

## Conclusion
This detailed analysis gives valuable insights into the essential skills required for data analysis roles. It highlights the importance of continuous learning and staying ahead in an evolving technological landscape. Through this project, I have learned many new techniques that have enhanced my understanding of data analysis. With these newfound insights I am eager to continue my journey, learning more techniques and refining my expertise in data analysis.
