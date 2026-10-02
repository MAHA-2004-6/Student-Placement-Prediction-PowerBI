# Student Placement Analytics – DAX Measures

## Table Name

`Full_dataset_student_placement_prediction_dataset_2026`

---

## 1. Student & Placement Measures

### Total Students

```DAX
Total Students =
COUNTROWS(Full_dataset_student_placement_prediction_dataset_2026)

Notes

Format Placement Rate and Internship Impact as Percentage in Power BI.

Format salary measures as Decimal Number and display them with the LPA label where appropriate.

If your Power BI table has a different name, replace in the formulas.

Dashboard Pages

Page 1 – Placement Overview

Uses placement KPIs, branch analysis, placement rate, salary and internship insights.

Page 2 – Placement Analysis

Uses placement rate and internship-related measures for deeper placement analysis.

Page 3 – Salary Analysis

Uses average salary, highest salary, median salary and placed-student measures.

Project: Student Placement Prediction & Analytics Dashboard
Tool: Microsoft Power BI
Language: DAX
