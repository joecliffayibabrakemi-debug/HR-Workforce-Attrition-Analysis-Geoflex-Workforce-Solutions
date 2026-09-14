# HR Workforce & Attrition Analysis

An HR analytics case study examining workforce structure, employee attrition, recruitment effectiveness, and data quality across Nigeria and Kenya.

> **Portfolio project:** A self directed case study using a provided HR dataset to simulate a junior Data Analyst assignment.

## Business Problem

Geoflex Workforce Solutions stores HR information across eight separate datasets. The data contains duplicate records, missing values, inconsistent formatting, and other quality issues.

The analysis focuses on three business questions:

1. Where is employee attrition highest?
2. Which recruitment sources produce the highest hire rates?
3. Which departments and branches require further HR attention?

## Executive Summary
 • **Attrition:** With the company recording a 14.5% overall attrition rate, I analyzed attrition across departments and branches to identify where retention concerns were concentrated. Customer Service had the highest departmental attrition at 18.3%, while Busia recorded the highest branch rate at 23.1%, compared with 7.4% in Ilorin. The 15.7 percentage-point gap showed that retention efforts should be targeted rather than applied uniformly across the workforce.

• **Recruitment:** To evaluate the effectiveness of recruitment channels, I calculated hire rates and compared high-volume sources to avoid drawing conclusions from smaller samples. Campus Recruitment (17.9%) and Company Website (17.3%) recorded higher hire rates than Job Portal (14.2%) and Indeed (12.5%) among the major channels. This provides a starting point for reviewing recruitment performance, although cost per hire and candidate quality would be needed before making budget decisions.

• **Exit Data Quality:** While analyzing employee tenure at exit, I identified 148 of 362 exit records (41%) with negative tenure values, meaning the recorded exit date occurred before the hire date. Since this is a fictional portfolio dataset, the cause cannot be confirmed, so I treated the values as a data-quality issue rather than employee behavior. I excluded these records from first-year retention interpretation and separately identified 100 employees (28%) who had valid exits within their first year. This prevented the invalid records from distorting the attrition analysis.

## Tech Stack & Tools

• **Microsoft Excel:** Data inspection, validation, duplicate checks, and exploratory analysis.

• **Power Query:** Data cleaning, transformation, formatting, and duplicate removal.

• **Power BI:** Data modeling, DAX measures, interactive dashboards, and data visualization.

• **DAX:** Attrition rate, hire rate, training completion, attendance, payroll, and year over year workforce measures.

• **PowerPoint:** for presenting findings and recommendations

• **AI tools:** for research, brainstorming, documentation, or workflow support

## Data Preparation & Quality

The project used eight HR tables:

`Employees`
`Attendance`
`ExitRecords`
`Recruitment`
`Promotions`
`TrainingRecords`
`PerformanceReviews`
`LeaveRequests`

I identified and removed **1,053 duplicate records** across the eight tables.

The Employees table contained missing Department IDs in 80 records, missing emails in 78 records, and missing phone numbers in 87 records.

I also standardized text formatting, cleaned date fields, filled Department IDs where reliable lookup information was available, and validated employee relationships before building the Power BI model.

The tables were connected through `EmployeeID`, with Department and Branch used as lookup dimensions.

## Key Visuals

### Executive Overview

<img width="2075" height="1200" alt="executive-overview" src="https://github.com/user-attachments/assets/7d06cb81-6acd-44dd-abc9-3616a1da51e0" />


### Attrition Analysis

<img width="2075" height="1200" alt="attrition-analysis" src="https://github.com/user-attachments/assets/06d0b515-df76-4014-b5e2-c8d07cbf95fb" />


### Talent Acquisition

<img width="2075" height="1200" alt="talent-acquisition" src="https://github.com/user-attachments/assets/21d2e437-3665-458e-97b7-f0b9d0a2c032" />


### Branch Comparison

<img width="2075" height="1200" alt="branch-comparison" src="https://github.com/user-attachments/assets/f06ae983-dd20-4304-bd15-8931c02d4782" />


## Key Insights

• Customer Service recorded the highest departmental attrition rate at 18.3%, while Supply Chain recorded 13.3%.

• Busia recorded the highest branch attrition rate at 23.1%, followed by Lokoja at 21.2%.

• Campus Recruitment recorded a 17.9% hire rate, compared with 12.5% for Indeed.

• Only 1.3% of performance reviews fell into the High performance category.

• Only 400 of 2,500 employees were marked as Active, while 1,072 were marked Terminated, Resigned, or Retired. This does not align with the 14.5% attrition KPI and requires data reconciliation.

• 148 exit records contained negative tenure values, indicating that some recorded exit dates occurred before the corresponding hire dates.

## Recommendations

1. Review retention factors in Customer Service, Administration, Busia, and Lokoja before introducing a company wide retention programme.

2. Compare recruitment costs alongside hire rates to determine whether high performing recruitment sources should receive more attention.

3. Investigate first year employee exits and review onboarding and early employee support.

4. Correct the negative tenure records and validate exit dates against employee hire dates.

5. Reconcile EmploymentStatus with ExitRecords so headcount and attrition reporting use consistent definitions.

## Project Challenges

The eight source tables contained 1,053 duplicate records, which could have inflated employee and transaction counts. I removed duplicates before analysis.

Several employee records contained missing values. I filled Department IDs where a reliable lookup was available and retained missing contact information rather than creating unsupported values.

The ExitRecords table contained 148 negative tenure values. I treated these as a data quality issue instead of including them in the early attrition calculation.

## Project Limitations

This project uses a provided instructional dataset and does not represent real Geoflex business operations.

The dataset does not contain enough cost information to calculate recruitment cost per hire or the financial impact of employee attrition.

The negative tenure records remain unresolved and therefore limit confidence in the complete exit tenure analysis.

## Business Value

The analysis helps identify where employee attrition is concentrated, compare recruitment sources by hiring efficiency, and identify data quality issues that could affect workforce reporting and planning.

## Repository Structure

```text
HR-Analytics/
│
├── README.md
│
├── images/
│   ├── executive-overview.png
│   ├── attrition-analysis.png
│   ├── talent-acquisition.png
│   └── branch-comparison.png
│
├── documentation/
│   ├── Problem_Statement.docx
│   └── Business_Questions.docx
│
├── data/
│   ├── raw/
│   └── cleaned/
│
└── dashboard/
    └── HR-Analytics.pbix
```
