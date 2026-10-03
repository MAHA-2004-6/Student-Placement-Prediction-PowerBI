# Student Placement Analytics – DAX Measures

## Table Name

`Full_dataset_student_placement_prediction_dataset_2026`

---

## 1. Student & Placement Measures

### Total Students

## Total Students

```DAX
Total Students =
COUNTROWS(
    Full_dataset_student_placement_prediction_dataset_2026
)
```

### Placed Students

```DAX
Placed Students =
CALCULATE(
    COUNTROWS(Full_dataset_student_placement_prediction_dataset_2026),
    Full_dataset_student_placement_prediction_dataset_2026[placement_status] = "Placed"
)
```
### Not Placed Students

```DAX
Not Placed Students =
[Total Students] - [Placed Students]
```
### Placement rate

```DAX
Placement Rate =
DIVIDE(
    [Placed Students],
    [Total Students],
    0
)
```
### Total Students Placed

```DAX
Total Students Placed =
CALCULATE(
    COUNTROWS(Full_dataset_student_placement_prediction_dataset_2026),
    Full_dataset_student_placement_prediction_dataset_2026[placement_status] = "Placed"
)
```
## 2. Salary Measures

### Average Salary (LPA)

```DAX
Average Salary (LPA) =
AVERAGE(
    Full_dataset_student_placement_prediction_dataset_2026[salary_package_lpa]
)
```
### Average Salary (Placed)

```DAX
Average Salary (Placed) =
CALCULATE(
    AVERAGE(
        Full_dataset_student_placement_prediction_dataset_2026[salary_package_lpa]
    ),
    Full_dataset_student_placement_prediction_dataset_2026[placement_status] = "Placed"
)
```
### Highest Salary (LPA)

```DAX
Highest Salary (LPA) =
MAX(
    Full_dataset_student_placement_prediction_dataset_2026[salary_package_lpa]
)
```
### Median Salary (LPA)

```DAX
Median Salary (LPA) =
CALCULATE(
    MEDIAN(
        Full_dataset_student_placement_prediction_dataset_2026[salary_package_lpa]
    ),
    Full_dataset_student_placement_prediction_dataset_2026[placement_status] = "Placed"
)
```
## 3. Branch Analysis Measures

### Top Branch

```DAX
Top Branch =
VAR T =
    ADDCOLUMNS(
        ALL(
            Full_dataset_student_placement_prediction_dataset_2026[branch]
        ),
        "PlacementRate",
        CALCULATE([Placement Rate])
    )
RETURN
    CONCATENATEX(
        TOPN(1, T, [PlacementRate], DESC),
        Full_dataset_student_placement_prediction_dataset_2026[branch],
        ", "
    )
```
### Top Branch Placement Rate

```DAX
Top Branch Placement Rate =
VAR T =
    ADDCOLUMNS(
        ALL(
            Full_dataset_student_placement_prediction_dataset_2026[branch]
        ),
        "PlacementRate",
        CALCULATE([Placement Rate])
    )
RETURN
    MAXX(
        TOPN(1, T, [PlacementRate], DESC),
        [PlacementRate]
    )
```
### Highest Avg Salary

```DAX
Highest Avg Salary =
VAR T =
    ADDCOLUMNS(
        ALL(
            Full_dataset_student_placement_prediction_dataset_2026[branch]
        ),
        "AvgSalary",
        CALCULATE([Average Salary (Placed)])
    )
RETURN
    MAXX(
        T,
        [AvgSalary]
    )
```
### Highest Avg Salary Branch

```DAX
Highest Avg Salary Branch =
VAR T =
    ADDCOLUMNS(
        ALL(
            Full_dataset_student_placement_prediction_dataset_2026[branch]
        ),
        "AvgSalary",
        CALCULATE([Average Salary (Placed)])
    )
RETURN
    CONCATENATEX(
        TOPN(1, T, [AvgSalary], DESC),
        Full_dataset_student_placement_prediction_dataset_2026[branch],
        ", "
    )
```
## 4. Internship Analysis

### Internship Impact

```DAX
Internship Impact =
VAR WithInternship =
    CALCULATE(
        [Placement Rate],
        Full_dataset_student_placement_prediction_dataset_2026[internships_count] > 0
    )
VAR WithoutInternship =
    CALCULATE(
        [Placement Rate],
        Full_dataset_student_placement_prediction_dataset_2026[internships_count] = 0
    )
RETURN
    WithInternship - WithoutInternship
```

## 5. CGPA Analysis

### CGPA Range

```DAX
CGPA Range =
SWITCH(
    TRUE(),
    Full_dataset_student_placement_prediction_dataset_2026[cgpa] < 6, "Below 6",
    Full_dataset_student_placement_prediction_dataset_2026[cgpa] < 7, "6–7",
    Full_dataset_student_placement_prediction_dataset_2026[cgpa] < 8, "7–8",
    Full_dataset_student_placement_prediction_dataset_2026[cgpa] < 9, "8–9",
    "9–10"
)
```
## 6. Coding Skill Analysis

### Coding Skill Range

```DAX
Coding Skill Range =
SWITCH(
    TRUE(),
    Full_dataset_student_placement_prediction_dataset_2026[coding_skill_score] <= 20, "0–20",
    Full_dataset_student_placement_prediction_dataset_2026[coding_skill_score] <= 40, "21–40",
    Full_dataset_student_placement_prediction_dataset_2026[coding_skill_score] <= 60, "41–60",
    Full_dataset_student_placement_prediction_dataset_2026[coding_skill_score] <= 80, "61–80",
    "81–100"
)
```

## 7. Communication Skill Analysis

### Communication Score Range

```DAX
Communication Score Range =
SWITCH(
    TRUE(),
    Full_dataset_student_placement_prediction_dataset_2026[communication_score] <= 20, "0–20",
    Full_dataset_student_placement_prediction_dataset_2026[communication_score] <= 40, "21–40",
    Full_dataset_student_placement_prediction_dataset_2026[communication_score] <= 60, "41–60",
    Full_dataset_student_placement_prediction_dataset_2026[communication_score] <= 80, "61–80",
    "81–100"
)
```

## 8. Salary Distribution

### Salary Range

```DAX
Salary Range =
SWITCH(
    TRUE(),
    Full_dataset_student_placement_prediction_dataset_2026[salary_package_lpa] < 3, "< 3 LPA",
    Full_dataset_student_placement_prediction_dataset_2026[salary_package_lpa] < 5, "3 – 5 LPA",
    Full_dataset_student_placement_prediction_dataset_2026[salary_package_lpa] < 7, "5 – 7 LPA",
    Full_dataset_student_placement_prediction_dataset_2026[salary_package_lpa] <= 10, "7 – 10 LPA",
    "> 10 LPA"
)
```
## Notes

Format Placement Rate and Internship Impact as Percentage in Power BI.

Format salary measures as Decimal Number and display them with the LPA label where appropriate.

If your Power BI table has a different name, replace in the formulas.

### Dashboard Pages

Page 1 – Placement Overview

Uses placement KPIs, branch analysis, placement rate, salary and internship insights.

Page 2 – Placement Analysis

Uses placement rate and internship-related measures for deeper placement analysis.

Page 3 – Salary Analysis

Uses average salary, highest salary, median salary and placed-student measures.

#### Project: Student Placement Prediction & Analytics Dashboard

#### Tool: Microsoft Power BI

#### Language: DAX
