# Chapter 1 — Introduction to Power BI, Architecture, and Core Concepts

## Microsoft Power BI Data Analyst Associate (PL-300)

---

# Chapter Objectives

After completing this chapter, learners should understand:

* What Power BI is and why organizations use it
* The components of the Power BI ecosystem
* Power BI Desktop vs Power BI Service
* The role of semantic models
* The difference between reports, dashboards, and apps
* The Power BI architecture hierarchy
* What tenants are and why they matter
* Capacity concepts
* Power Query vs DAX responsibilities
* Basic security concepts
* Core PL-300 terminology

---

# 1.1 What Is Power BI?

Power BI is Microsoft's business intelligence platform used to:

* Connect to data
* Transform and clean data
* Build data models
* Create calculations
* Design interactive reports
* Share insights with users

Power BI allows organizations to turn raw data into actionable information.

Example:

Raw Data:

```
Sales Transactions
Customer Information
Product Data
```

↓

Power BI

↓

Business Insights:

```
Revenue Trends
Customer Analysis
Product Performance
```

---

# 1.2 The Power BI Workflow

The typical Power BI workflow is:

```id="3q6h4m"
Data Sources

↓

Power Query

↓

Semantic Model

↓

Reports

↓

Dashboards / Apps
```

Each stage has a different purpose.

---

# 1.3 Power BI Components

Power BI consists of several major components.

---

# Power BI Desktop

Power BI Desktop is the development application.

Used for:

* Connecting to data
* Transforming data
* Creating relationships
* Creating measures
* Writing DAX
* Building reports

Think:

> Where analysts build Power BI solutions.

---

# Power BI Service

Power BI Service is the cloud platform.

Used for:

* Publishing reports
* Sharing content
* Managing workspaces
* Creating apps
* Scheduling refreshes
* Managing security

Think:

> Where organizations distribute and manage Power BI solutions.

---

# Power BI Mobile

Used for:

* Viewing reports
* Monitoring dashboards
* Accessing business insights on mobile devices

---

# Component Comparison

| Component        | Purpose                  |
| ---------------- | ------------------------ |
| Power BI Desktop | Build models and reports |
| Power BI Service | Publish, share, manage   |
| Power BI Mobile  | Consume reports          |

---

# PL-300 Exam Scenario

A developer needs to create relationships between tables.

Where should this be done?

Correct:

✅ Power BI Desktop

---

A manager needs access to a published report.

Where would they access it?

Correct:

✅ Power BI Service

---

# 1.4 Semantic Models

A semantic model is the foundation of Power BI reporting.

A semantic model contains:

* Tables
* Relationships
* Measures
* Calculated columns
* Calculated tables
* Security roles

The semantic model stores the business logic used by reports.

---

# Semantic Model Architecture

Example:

```
Data Sources

↓

Semantic Model

    Tables
    Relationships
    Measures
    Security

↓

Reports
```

---

# Semantic Model vs Report

This is a common PL-300 distinction.

| Semantic Model         | Report               |
| ---------------------- | -------------------- |
| Stores data structure  | Displays information |
| Contains relationships | Contains visuals     |
| Contains measures      | Uses measures        |
| Contains security      | Uses model security  |

---

# Exam Trap

A report contains relationships and DAX measures.

❌ Incorrect

Relationships and measures belong to:

✅ Semantic model

---

# 1.5 Reports, Dashboards, and Apps

These terms are often confused.

---

# Reports

Reports are interactive collections of visuals.

Characteristics:

* Multiple pages
* Built in Power BI Desktop
* Connect to semantic models
* Allow filtering and analysis

Example:

Sales Report:

* Overview page
* Product page
* Customer page

---

# Dashboards

Dashboards are single-page monitoring views.

Characteristics:

* Created in Power BI Service
* Contain pinned tiles
* Can combine visuals from multiple reports

Example:

Executive Dashboard:

* Revenue KPI
* Sales Target
* Profit Indicator

---

# Apps

Apps distribute Power BI content to users.

Used for:

* Publishing finished solutions
* Controlled distribution
* Organizational reporting

Example:

Sales App:

Contains:

* Sales Dashboard
* Regional Reports
* Forecast Reports

---

# Report vs Dashboard vs App

| Feature              | Report | Dashboard | App     |
| -------------------- | ------ | --------- | ------- |
| Multiple pages       | ✅      | ❌         | Depends |
| Built in Desktop     | ✅      | ❌         | ❌       |
| Interactive analysis | ✅      | Limited   | Depends |
| Distribution method  | ❌      | ❌         | ✅       |

---

# 1.6 Power BI Tenant

A tenant is the organization's Power BI environment.

Think:

> Tenant = The organization's Power BI container.

A tenant contains:

* Users
* Workspaces
* Reports
* Semantic models
* Security settings
* Governance settings

Example:

```
Company Tenant

|
+-- Sales Workspace
|
+-- Finance Workspace
|
+-- HR Workspace
```

---

# Tenant vs Workspace

| Tenant                          | Workspace                  |
| ------------------------------- | -------------------------- |
| Entire organization environment | Collaboration area         |
| Highest level boundary          | Contains content           |
| Managed by administrators       | Managed by workspace roles |

---

# Security Hierarchy

Power BI security happens at multiple levels.

```
Tenant

↓

Workspace Permissions

↓

Semantic Model Permissions

↓

Row-Level Security
```

---

# Tenant Settings

Tenant administrators control organization-wide settings.

Examples:

* External sharing
* Workspace creation
* Export permissions
* Developer features

---

# PL-300 Scenario

A company wants to prevent users from sharing reports externally.

Where should this be configured?

Correct:

✅ Tenant settings

---

# 1.7 Power BI Capacity

Capacity determines the resources available for Power BI workloads.

---

# Shared Capacity

Default environment.

Characteristics:

* Resources are shared
* Has limitations
* Common with Power BI Pro

---

# Premium/Fabric Capacity

Dedicated organizational resources.

Benefits:

* More processing power
* Larger workloads
* More scalability

---

# Capacity vs Tenant

A tenant is the organization.

Capacity provides computing resources.

Example:

```
Tenant

↓

Capacity

↓

Workspaces

↓

Reports
```

---

# 1.8 Power Query vs DAX

A major PL-300 concept is knowing when to use each.

---

# Power Query

Used before data enters the model.

Purpose:

* Clean data
* Transform data
* Combine data

Examples:

* Remove duplicates
* Change data types
* Merge tables
* Append tables
* Pivot/unpivot

Language:

✅ M

---

# DAX

Used after data is loaded.

Purpose:

* Create calculations
* Analyze data

Examples:

* Measures
* Calculated columns
* Time intelligence

Language:

✅ DAX

---

# Power Query vs DAX

| Power Query          | DAX                  |
| -------------------- | -------------------- |
| Data preparation     | Data analysis        |
| Before loading       | After loading        |
| M language           | DAX language         |
| Creates clean tables | Creates calculations |

---

# PL-300 Decision Guide

Need to:

Remove duplicates?

✅ Power Query

Need to:

Calculate year-over-year growth?

✅ DAX Measure

Need to:

Create a profit calculation?

Usually:

✅ DAX Measure

---

# 1.9 Basic Power BI Security Concepts

Security in Power BI has multiple layers.

---

# Tenant Security

Controls:

* Who can use Power BI
* Organization settings

---

# Workspace Security

Controls:

* Who can edit content
* Who can publish content

Examples:

* Admin
* Member
* Contributor
* Viewer

---

# Semantic Model Security

Controls:

* Data access

Example:

Row-Level Security:

Salesperson sees only their customers.

---

# 1.10 Common PL-300 Exam Traps

---

## Trap 1

Datasets and semantic models are different concepts.

❌ Incorrect

Microsoft now refers to datasets as:

✅ Semantic models

---

## Trap 2

Power BI Desktop is used for sharing reports.

❌ Incorrect

Desktop builds reports.

Service shares them.

---

## Trap 3

Dashboards contain multiple report pages.

❌ Incorrect

Dashboards are single-page canvases.

---

## Trap 4

RLS controls who can open reports.

❌ Incorrect

RLS controls what data users see.

---

## Trap 5

Power Query and DAX perform the same tasks.

❌ Incorrect

Power Query prepares data.

DAX analyzes data.

---

# Chapter 1 Practice Exam Questions

---

# Question 1

A data analyst needs to create relationships between tables.

Where should this task be performed?

A. Power BI Service

B. Power BI Desktop

C. Power BI Mobile

D. Dashboard

Correct Answer:

✅ B. Power BI Desktop

---

# Question 2

Which component stores relationships, measures, and security roles?

A. Report

B. Dashboard

C. Semantic Model

D. Workspace

Correct Answer:

✅ C. Semantic Model

---

# Question 3

An administrator wants to prevent users from sharing reports outside the organization.

Where should this be configured?

A. Report filter

B. Tenant settings

C. Visual settings

D. Bookmark

Correct Answer:

✅ B. Tenant settings

---

# Question 4

A developer needs to remove duplicate records before loading data.

What should they use?

A. DAX

B. Power Query

C. Measure

D. Relationship

Correct Answer:

✅ B. Power Query

---

# Question 5

A manager wants a single page showing important KPIs from multiple reports.

What should they use?

A. Report

B. Dashboard

C. Semantic Model

D. Dataflow

Correct Answer:

✅ B. Dashboard

---

# Question 6

A company wants to distribute finalized reports to hundreds of employees.

What should they use?

A. Workspace

B. App

C. Calculated column

D. Gateway

Correct Answer:

✅ B. App

---

# Chapter 1 Summary

Remember the Power BI hierarchy:

```
Tenant

↓

Capacity

↓

Workspace

↓

Semantic Model

↓

Report

↓

App / Dashboard
```

Core concepts:

| Concept        | Purpose                  |
| -------------- | ------------------------ |
| Desktop        | Build solutions          |
| Service        | Publish and share        |
| Semantic Model | Store data logic         |
| Report         | Analyze data             |
| Dashboard      | Monitor KPIs             |
| App            | Distribute content       |
| Tenant         | Organization environment |
| Power Query    | Prepare data             |
| DAX            | Calculate insights       |

---

# Next Chapter

## Chapter 2 — Connecting to Data Sources and Power Query

Topics:

* Data connectors
* Import mode
* DirectQuery introduction
* Data transformation
* Query folding
* Parameters
* Merge vs Append
* Data types
* Data gateways
* PL-300 connectivity scenarios
