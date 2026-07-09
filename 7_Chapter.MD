# Chapter 7 — Advanced Analytics, Optimization, and Publishing Concepts

## Microsoft Power BI Data Analyst Associate (PL-300)

---

# Chapter Objectives

After completing this chapter, learners should understand:

* Advanced Power BI analytical features
* What-if parameters
* Q&A and Smart Narrative
* Analyze in Excel
* Performance Analyzer
* Report optimization
* Query reduction
* Publishing workflow
* Reports vs dashboards vs apps
* Workspace concepts

---

# 7.1 Advanced Analytics in Power BI

Power BI includes tools that help users move beyond descriptive reporting.

Traditional reporting answers:

> What happened?

Advanced analytics helps answer:

> Why did it happen?

and

> What could happen?

---

# 7.2 What-If Parameters

A What-if parameter allows users to interactively change a value and see how results change.

Example:

A company wants to see:

"What happens if we increase prices by 5%?"

Create:

Price Increase Parameter

Values:

0% - 20%

---

# How It Works

Power BI creates:

1. A parameter table
2. A slicer
3. A measure

---

Example:

Parameter:

5%

Calculation:

```DAX
Adjusted Sales =
[Total Sales] *
(1 + [Price Increase])
```

---

# Common Uses

* Pricing scenarios
* Budget planning
* Forecasting
* Sensitivity analysis

---

# PL-300 Scenario

A manager wants to adjust a discount percentage and see updated profit.

Use:

✅ What-if parameter

---

# 7.3 Q&A Visual

The Q&A visual allows users to ask questions using natural language.

Example:

User types:

"Sales by region"

Power BI creates a visual.

---

# Requirements

Works best when:

* Data model is well designed
* Columns have meaningful names
* Relationships are correct

---

# Improving Q&A Results

Use:

* Synonyms
* Friendly column names
* Good modeling practices

---

# PL-300 Scenario

A business user wants to type questions instead of building visuals.

Use:

✅ Q&A visual

---

# 7.4 Smart Narrative

Smart Narrative automatically creates text summaries.

Example:

"Sales increased 12% compared to last month."

---

# Uses

Good for:

* Executive summaries
* Automated explanations

---

# Limitations

It does not replace:

* Data analysis
* Business decisions

---

# 7.5 Analyze in Excel

Analyze in Excel allows users to connect Excel to a Power BI semantic model.

---

# Benefits

Users can:

* Use PivotTables
* Analyze enterprise data
* Keep a single source of truth

---

# Requirements

Users need appropriate permissions.

---

# PL-300 Scenario

An analyst wants to create Excel PivotTables using a Power BI dataset.

Use:

✅ Analyze in Excel

---

# 7.6 Performance Analyzer

Performance Analyzer identifies report performance issues.

Located in:

Power BI Desktop

View → Performance Analyzer

---

# What It Measures

Includes:

* Visual display time
* DAX query time
* Other processing time

---

# Example

A report is slow.

Performance Analyzer shows:

Visual 1:

10 seconds

Visual 2:

0.5 seconds

---

The analyst investigates Visual 1.

---

# Important:

Performance Analyzer:

Does:

✅ Identify bottlenecks

Does NOT:

❌ Automatically optimize reports

---

# 7.7 Report Optimization Techniques

---

# Reduce Number of Visuals

Every visual generates queries.

Too many visuals:

* Slow rendering
* More queries

---

# Reduce Data Model Size

Remove:

* Unused columns
* Unnecessary rows

---

# Use Measures

Prefer:

Measures

over:

Many calculated columns

---

# Optimize Relationships

Avoid:

* Unnecessary relationships
* Complex many-to-many designs

---

# Use Star Schema

Improves:

* Performance
* Usability

---

# 7.8 Query Reduction

Query reduction controls how often visuals send queries.

Useful for:

DirectQuery models.

---

# Options Include:

## Apply Button

Allows users to select multiple slicer values before querying.

---

Example:

Without Apply:

User selects:

5 filters

=

5 queries

---

With Apply:

5 selections

=

1 query

---

# PL-300 Scenario

A DirectQuery report performs poorly because slicers trigger too many queries.

Use:

✅ Query reduction

---

# 7.9 Publishing Reports

Power BI Desktop creates reports.

Power BI Service hosts and shares them.

---

# Publishing Flow

```text
Power BI Desktop

↓

Workspace

↓

Report

↓

Users
```

---

# Report

Contains:

* Visuals
* Pages
* Filters

---

# Semantic Model

Contains:

* Tables
* Relationships
* Measures

---

# Dashboard

Contains:

* Tiles
* KPIs
* Visual summaries

---

# App

Packages content for distribution.

---

# 7.10 Report vs Dashboard vs App

| Feature              | Report  | Dashboard | App     |
| -------------------- | ------- | --------- | ------- |
| Created in Desktop   | Yes     | No        | No      |
| Multiple pages       | Yes     | No        | No      |
| Multiple visuals     | Yes     | Tiles     | Yes     |
| Interactive analysis | Yes     | Limited   | Depends |
| Distribution         | Limited | Limited   | Best    |

---

# PL-300 Trap

A dashboard is just a one-page report.

❌ Incorrect

Dashboards are Service-only collections of tiles.

---

# 7.11 Workspaces Introduction

A workspace is a collaboration area in Power BI Service.

Used for:

* Developing content
* Sharing content
* Managing permissions

---

# Workspace Contains:

* Reports
* Semantic models
* Dashboards
* Dataflows
* Apps

---

# 7.12 Publishing an App

Apps distribute finalized content.

Example:

Sales Analytics App

Contains:

* Sales reports
* Dashboards
* Documentation

---

# Benefits:

* Controlled distribution
* Easier updates
* User-friendly experience

---

# App vs Workspace

Workspace:

For creators.

App:

For consumers.

---

# 7.13 Common PL-300 Exam Traps

---

## Trap 1

Performance Analyzer fixes slow reports.

❌ Incorrect

It identifies problems.

---

## Trap 2

Dashboards are created in Power BI Desktop.

❌ Incorrect

Dashboards are Power BI Service objects.

---

## Trap 3

Apps are where developers build reports.

❌ Incorrect

Workspaces are for development.

---

## Trap 4

Q&A works best with poor naming conventions.

❌ Incorrect

Good modeling improves Q&A.

---

## Trap 5

What-if parameters modify source data.

❌ Incorrect

They simulate scenarios inside the model.

---

## Trap 6

Analyze in Excel creates a copy of the data.

❌ Incorrect

It connects to the semantic model.

---

# Chapter 7 Practice Questions

---

# Question 1

A manager wants to change a discount percentage and immediately see updated profit.

What should be created?

A. Bookmark

B. What-if parameter

C. Drillthrough

D. Dashboard

Correct Answer:

✅ B. What-if parameter

---

# Question 2

A report is slow. An analyst needs to identify which visual takes the longest to load.

What should be used?

A. Query Editor

B. Performance Analyzer

C. Gateway

D. Deployment Pipeline

Correct Answer:

✅ B. Performance Analyzer

---

# Question 3

A user wants Excel PivotTables connected directly to a Power BI semantic model.

Which feature should be used?

A. Export data

B. Analyze in Excel

C. Smart Narrative

D. Q&A

Correct Answer:

✅ B. Analyze in Excel

---

# Question 4

A company wants to provide finalized reports to hundreds of users.

What should be created?

A. Workspace

B. App

C. Dataset copy

D. Dashboard

Correct Answer:

✅ B. App

---

# Question 5

A DirectQuery report has performance issues caused by frequent slicer changes.

What should be configured?

A. Query reduction

B. Conditional formatting

C. Bookmarks

D. Hierarchies

Correct Answer:

✅ A. Query reduction

---

# Question 6

A user wants to ask questions using natural language.

Which feature should they use?

A. Q&A

B. Drillthrough

C. Matrix

D. Bookmark

Correct Answer:

✅ A. Q&A

---

# Chapter 7 Summary

| Concept              | Purpose                         |
| -------------------- | ------------------------------- |
| What-if Parameter    | Scenario analysis               |
| Q&A                  | Natural language questions      |
| Smart Narrative      | Automated summaries             |
| Analyze in Excel     | Excel access to semantic models |
| Performance Analyzer | Find bottlenecks                |
| Query Reduction      | Reduce unnecessary queries      |
| Report               | Interactive analysis            |
| Dashboard            | Service tiles                   |
| Workspace            | Development collaboration       |
| App                  | Content distribution            |

---

# Next Chapter

## Chapter 8 — Power BI Service, Security, Sharing, and Administration

Topics:

* Workspaces
* Roles
* Permissions
* Viewer vs Member vs Contributor vs Admin
* Apps
* Sharing
* Row-Level Security
* Gateways
* Refresh
* Deployment concepts
* Tenant settings
* PL-300 security scenarios
