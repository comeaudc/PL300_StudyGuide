# Chapter 9 — PL-300 Final Review and Scenario Practice

## Microsoft Power BI Data Analyst Associate (PL-300)

---

# How Microsoft Tests the PL-300

The PL-300 is not primarily a memorization exam.

Microsoft typically gives:

* A business requirement
* A technical limitation
* Several possible solutions

Your job:

Choose the solution that best satisfies the requirement.

---

# Exam Decision Framework

When reading questions, ask:

## 1. Is this a data preparation problem?

Think:

Power Query

Examples:

* Cleaning data
* Removing columns
* Combining tables
* Changing types

---

## 2. Is this a modeling problem?

Think:

Semantic Model

Examples:

* Relationships
* Star schema
* Measures
* Date tables

---

## 3. Is this an analysis problem?

Think:

Reports and visuals

Examples:

* Charts
* Drillthrough
* Tooltips
* AI visuals

---

## 4. Is this a deployment/security problem?

Think:

Power BI Service

Examples:

* Workspaces
* Apps
* Permissions
* Refresh
* RLS

---

# Case Study 1 — Retail Sales Model

## Scenario

A company stores sales data in SQL Server.

The dataset contains:

* 500 million sales transactions
* Customer table
* Product table
* Date table

The company needs:

* Daily reporting
* Fast dashboards
* Minimal refresh time

---

## Question 1

Which storage mode should be used for the Sales table?

A. Import

B. DirectQuery

C. Dual

D. Live Connection

### Correct Answer:

✅ B. DirectQuery

### Explanation:

The dataset is extremely large and requires current data.

DirectQuery allows Power BI to query the source.

---

Why not:

A. Import

❌ Large datasets may exceed practical limits.

C. Dual

❌ Usually used for dimension tables in composite models.

D. Live Connection

❌ Used when connecting to existing semantic models.

---

# Question 2

Customer and Product tables should be optimized for performance.

Which storage mode should they use?

A. Import

B. DirectQuery

C. Dual

D. None

### Correct Answer:

✅ C. Dual

### Explanation:

In composite models, dimensions often use Dual mode so they can efficiently interact with both Import and DirectQuery tables.

---

# Case Study 2 — Power Query Cleaning

## Scenario

An Excel file contains:

| Jan | Feb | Mar |
| --- | --- | --- |
| 100 | 200 | 300 |

The analyst wants to create a proper sales model.

---

# Question 3

Which transformation should be performed?

A. Pivot

B. Unpivot

C. Merge

D. Append

### Correct Answer:

✅ B. Unpivot

### Explanation:

Monthly columns should become rows.

---

# Question 4

The analyst wants to remove invalid records before loading data.

Where should this happen?

A. Report filter

B. DAX measure

C. Power Query

D. Visual filter

### Correct Answer:

✅ C. Power Query

---

# Case Study 3 — DAX

## Scenario

A company needs:

Total Sales

and

Sales Percentage of Total

---

# Question 5

Which function is commonly used to remove filters for percentage calculations?

A. SUMX

B. ALL

C. VALUES

D. COUNTROWS

### Correct Answer:

✅ B. ALL

---

# Question 6

A measure must calculate sales only for the current year.

Which function should be used?

A. CALCULATE

B. SUM

C. DISTINCT

D. RELATED

### Correct Answer:

✅ A. CALCULATE

---

# Case Study 4 — Relationships

## Scenario

A company creates this model:

Customer

↓

Sales

↓

Product

---

# Question 7

What relationship should exist between Customer and Sales?

A. Many-to-many

B. One-to-many

C. One-to-one

D. No relationship

### Correct Answer:

✅ B. One-to-many

---

# Question 8

A report requires comparing:

Order Date

and

Ship Date

What should be used?

A. Duplicate Sales table

B. USERELATIONSHIP()

C. Bidirectional filtering

D. Many-to-many relationship

### Correct Answer:

✅ B. USERELATIONSHIP()

---

# Case Study 5 — Visual Selection

## Scenario

A manager asks:

"Which factors influence customer churn?"

---

# Question 9

Which visual should be used?

A. Key Influencers

B. Pie Chart

C. Card

D. Matrix

### Correct Answer:

✅ A. Key Influencers

---

# Question 10

A manager asks:

"Why did revenue decrease?"

They want to explore:

Region → Product → Store

Which visual?

A. Decomposition Tree

B. Q&A

C. Line Chart

D. Tooltip

### Correct Answer:

✅ A. Decomposition Tree

---

# Case Study 6 — Workspace Security

## Scenario

A company has:

Developers

Report creators

Consumers

---

# Question 11

A developer needs to create reports but should not manage users.

Which workspace role?

A. Viewer

B. Contributor

C. Member

D. Admin

### Correct Answer:

✅ B. Contributor

---

# Question 12

A user needs to publish a Power BI app.

Which role?

A. Viewer

B. Contributor

C. Member

D. None

### Correct Answer:

✅ C. Member

---

# Case Study 7 — Row-Level Security

## Scenario

Regional managers should only see their own region.

---

# Question 13

What should be implemented?

A. Filters

B. Bookmarks

C. Row-Level Security

D. Apps

### Correct Answer:

✅ C. Row-Level Security

---

# Case Study 8 — Refresh

## Scenario

A report uses an on-premises SQL Server database.

The dataset fails refreshing in Power BI Service.

---

# Question 14

What should be configured?

A. Gateway

B. Bookmark

C. Workspace

D. Dashboard

### Correct Answer:

✅ A. Gateway

---

# Case Study 9 — Performance

## Scenario

A DirectQuery report is slow.

The analyst wants to identify which visual causes the issue.

---

# Question 15

Which tool should be used?

A. Query Editor

B. Performance Analyzer

C. Model View

D. Data View

### Correct Answer:

✅ B. Performance Analyzer

---

# Final PL-300 High Value Rules

## Power Query

Remember:

Cleaning = Power Query

---

## Modeling

Remember:

Star schema

Fact = events

Dimension = descriptions

---

## DAX

Remember:

Measures = dynamic calculations

CALCULATE = changes filters

SUMX = row-by-row calculation

---

## Visuals

Remember:

Drill down:

Same visual

Drillthrough:

Different page

---

## Service

Remember:

Contributor:

Creates content

Member:

Can manage apps

Admin:

Controls workspace

---

## Security

Remember:

RLS filters data rows

Workspace roles control access

---

# Final Exam Checklist

Before taking PL-300, know:

✅ Import vs DirectQuery
✅ Composite vs Dual
✅ Query folding
✅ Merge vs Append
✅ Reference vs Duplicate
✅ Star schema
✅ Relationships
✅ Cardinality
✅ Filter direction
✅ Measures vs columns
✅ CALCULATE
✅ Time intelligence
✅ Visual selection
✅ Drillthrough vs drill down
✅ Key Influencers
✅ Decomposition Tree
✅ Workspace roles
✅ Apps
✅ RLS
✅ Gateway
✅ Refresh
✅ Tenant settings

---

# Final Recommendation

The highest-value review order before the exam:

1. Workspace roles/security
2. DAX context and CALCULATE
3. Storage modes
4. Relationships/modeling
5. Power Query transformations
6. Visual feature selection

These areas produce the most scenario-based questions.