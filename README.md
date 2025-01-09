
# HR Analytics Report  

![HR Report Cover](https://github.com/user-attachments/assets/7de34937-ba39-4085-965e-02a7c348394d)

## Overview  

Welcome to the HR Analytics Dashboard project! This Power BI dashboard is designed to empower HR teams with actionable insights into workforce demographics, employee retention, turnover, and headcount trends. The interactive visualizations enable stakeholders to make data-driven decisions for improving organizational efficiency, reducing turnover, and planning workforce strategies.  

## Problem Statement  

The primary objectives of this project are:  
- Track employee headcount trends over time.  
- Analyze employee turnover by job level, department, and demographics.  
- Identify key factors contributing to employee departures.  
- Measure employee retention and turnover rates.  
- Provide an interactive dashboard for HR stakeholders to slice and dice data across various dimensions.  

## Features  

- **Dynamic Headcount Analysis:** Monitor active employees by job level, department, and location.  
- **Turnover Insights:** Analyze turnover trends, reasons for departures, and termination types.  
- **Retention Metrics:** Track retention rates over time and identify key retention drivers.  
- **Demographic Breakdown:** Visualize workforce data by gender, age, and remote/on-site work distribution.  
- **Top/Bottom Earners Analysis:** Conditional formatting to highlight the highest and lowest earners.  
- **Interactive Filters and Tooltips:** Enable slicing data and providing contextual insights across dimensions.  

## Steps Followed  

### 1. **Data Preparation in Power Query**  
- Imported raw data into Power BI using Power Query.  
- Cleaned and transformed datasets to standardize formats, fill missing values, and remove duplicates.  
- Established relationships between fact and dimension tables for a robust data model.  

### 2. **Data Model Creation**  
- Built a star schema for efficient querying and analysis.  
- Defined key relationships between employee fact tables and supporting dimensions like date, department, and job level.

![Data Model](https://github.com/user-attachments/assets/16afb06d-b33e-460f-98e1-8f57aef43da4)

### 3. **DAX Measures Development**  
Developed advanced DAX measures to calculate key metrics. Below are some of the key DAX measures used in the project:  

#### **Headcount**  
```DAX  
Headcount =  
CALCULATE(  
    [All_Employees],  
    FILTER(  
        people_fact,  
        people_fact[hire_date] <= LASTDATE('Date'[Date]) &&  
        (  
            people_fact[term_date] > LASTDATE('Date'[Date]) ||  
            ISBLANK(people_fact[term_date])  
        )  
    )  
)  
```  

#### **Starting Headcount**  
```DAX  
Starting Headcount =  
CALCULATE(  
    [All_Employees],  
    FILTER(  
        people_fact,  
        people_fact[hire_date] < FIRSTDATE('Date'[Date]) &&  
        (ISBLANK(people_fact[term_date]) || people_fact[term_date] >= FIRSTDATE('Date'[Date]))  
    )  
)  
```  

#### **Ending Headcount**  
```DAX  
Ending Headcount =  
CALCULATE(  
    [All_Employees],  
    FILTER(  
        people_fact,  
        people_fact[hire_date] < FIRSTDATE('Date'[Date]) &&  
        (ISBLANK(people_fact[term_date]) || people_fact[term_date] >= LASTDATE('Date'[Date]))  
    )  
)  
```  

#### **Retention Rate**  
```DAX  
Retention =  
DIVIDE(  
    [Ending Headcount],  
    [Starting Headcount],  
    0  
) * 100  
```  

#### **Departing Employees**  
```DAX  
Departing Employees =  
CALCULATE(  
    [All_Employees],  
    FILTER(  
        people_fact,  
        people_fact[term_date] >= FIRSTDATE('Date'[Date]) &&  
        people_fact[term_date] <= LASTDATE('Date'[Date])  
    )  
)  
```  

#### **Turnover %**  
```DAX  
Turnover % =  
DIVIDE(  
    [Departing Employees],  
    [Avg # of Employees],  
    0  
) * 100  
```  

### 4. **Dashboard Creation**  
- Designed an intuitive and visually appealing dashboard in Power BI.  
- Incorporated dynamic slicers and filters for user interactivity.  
- Added tooltips for contextual information on metrics and visual elements.  
 

### 5. **Conditional Formatting**  
![Headcount conditional](https://github.com/user-attachments/assets/66539b44-bbbf-4084-b38b-063b9fc4c969)
- Applied formatting to highlight top 20 earners and bottom 20 earners based on salary.  
- Designed a clean and contrasting color scheme to differentiate key metrics and insights.  

## Key Components  

### 1. **Headcount View**  
![Headcount1](https://github.com/user-attachments/assets/0cbbb28f-4f86-462f-b4a8-f6777ec1be2f)  
- Total headcount by job level, department, and remote/on-site status.  
- Gender and age breakdown for workforce demographics.  
- Top and bottom salary earners with conditional formatting for quick identification.  

### 2. **Retention View**  
![Retention](https://github.com/user-attachments/assets/d0f8ca81-8a3a-46d0-b2da-7f4f6bdea468)  
- Year-on-year retention trends.  
- Min-Max Retention metrics to highlight best and worst-performing years.  
- Insights into factors affecting retention across job levels and demographics.  

### 3. **Turnover Analysis** 
![Turnover](https://github.com/user-attachments/assets/000a8f85-b18f-477e-97d1-fa6964977ea5) 
- Employee turnover rates over time, segmented by job level and department.  
- Reasons for employee departures (e.g., better opportunities, personal reasons, performance).  
- Voluntary vs. involuntary terminations visualized as a stacked bar chart.  

### 4. **Tooltips and Filters**  
![headcount tooltip](https://github.com/user-attachments/assets/1209c112-ec29-4968-9d4d-cd56fd9a4ee1)


![Filter Panel](https://github.com/user-attachments/assets/51ed7e8b-57de-4ee1-9a7c-d24fc42d51b4)
- Interactive filters to slice data by year, department, gender, job level, and more.  
- Tooltips providing contextual insights when hovering over visualizations.  

## Tech Stack  

- **Power BI:** Data visualization and dashboard creation.  
- **DAX (Data Analysis Expressions):** Advanced calculations for headcount, retention, and turnover.  
- **Power Query:** Data extraction, cleaning, and transformation.  

## Insights and Recommendations  

The HR Analytics Dashboard delivers actionable insights to HR leaders and decision-makers:  
- **Retention Strategies:** Identify factors driving employee retention and address critical issues for improvement.  
- **Turnover Reduction:** Analyze turnover trends and implement targeted interventions to reduce churn.  
  
- **Workforce Planning:** Use headcount trends to plan for hiring needs and align workforce strategy with organizational goals. 

## Detailed Insights
**Demographic Trends:**

**61%** of employees are male, with the largest age group between **25–34 years**.
Remote work adoption is at 20%, with 80% of employees on-site.

**Turnover Drivers:**

Customer Service has the highest turnover **(36.4%)**.
Key reasons for departure include better career opportunities and personal reasons.

**Retention Metrics:**

Retention rates have shown a steady improvement, reaching **97.3%** in 2019.

## Usage  

- Open the Power BI report file.  
- Select a timeframe using the date slicer.  
- Use the filter toolbox to explore specific dimensions like department, gender, or job level.  
- Hover over visual elements to access additional insights via tooltips.  

## Video Demo  

Watch the demo of the HR Analytics Dashboard:  
[![HR Analytics Demo](https://example.com/hr-demo-thumbnail.png)](https://youtu.be/gSWSXO7F-zE)  

## Conclusion  

The HR Analytics Dashboard demonstrates how data-driven insights can transform workforce management strategies. By analyzing headcount, retention, and turnover trends, organizations can proactively address challenges and optimize their HR practices. Explore the interactive dashboard to unlock the potential of data in shaping your workforce strategy!  



