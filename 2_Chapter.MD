# Chapter 2 — Connecting to Data Sources and Power Query

## Microsoft Power BI Data Analyst Associate (PL-300)

---

# Chapter Objectives

After completing this chapter, learners should understand:

* How Power BI connects to different data sources
* The difference between connectors and storage modes
* Import vs DirectQuery fundamentals
* Power Query's role in data preparation
* Query transformations
* Query folding
* Merge vs Append
* Data profiling
* Parameters
* Data gateways
* Common PL-300 connectivity scenarios

---

# 2.1 Connecting to Data Sources

Power BI can connect to many different types of data sources.

Common sources include:

## Files

Examples:

* Excel
* CSV
* XML
* JSON
* PDF

---

## Databases

Examples:

* SQL Server
* PostgreSQL
* Oracle
* MySQL

---

## Microsoft Services

Examples:

* SharePoint
* Dataverse
* Azure services

---

## Online Services

Examples:

* Salesforce
* Google Analytics

---

# 2.2 Connectors vs Storage Modes

A common PL-300 confusion is mixing these concepts.

They answer different questions.

---

# Connector

Question answered:

> "Where does my data come from?"

Examples:

* Excel connector
* SQL Server connector
* SharePoint connector

---

# Storage Mode

Question answered:

> "How does Power BI interact with the data?"

Examples:

* Import
* DirectQuery
* Dual

---

Example:

A report can use:

SQL Server Connector

*

Import Storage Mode

OR

SQL Server Connector

*

DirectQuery Storage Mode

---

# 2.3 Import Mode

Import mode loads data into the Power BI semantic model.

Process:

```id="8ok5as"
Data Source

↓

Power BI

↓

In-Memory Model

↓

Reports
```

---

# Advantages

✅ Fast report performance
✅ Full DAX functionality
✅ Full modeling capabilities
✅ Data compression

---

# Disadvantages

❌ Data is not automatically current
❌ Requires refresh

---

# Refresh Process

Example:

```id="7l1b7f"
Database

↓

Scheduled Refresh

↓

Updated Semantic Model
```

---

# PL-300 Scenario

A company needs fast dashboards and can refresh data every night.

Best choice:

✅ Import mode

---

# 2.4 DirectQuery Mode

DirectQuery does not import the data.

Instead:

Power BI sends queries directly to the source.

Example:

```id="3wv5la"
Report Interaction

↓

Power BI

↓

Database Query

↓

Source Database
```

---

# Advantages

✅ Near real-time data
✅ Data stays in source system
✅ Useful for very large datasets

---

# Disadvantages

❌ Slower performance
❌ More source dependency
❌ Some modeling limitations

---

# PL-300 Scenario

A company has billions of transaction rows and requires near real-time reporting.

Best choice:

✅ DirectQuery

---

# 2.5 Dual Storage Mode

Dual mode allows a table to behave as:

* Import
* DirectQuery

depending on the query.

Used mainly for:

* Composite models
* Performance optimization

---

# Example

Dimension table:

Customer

Storage Mode:

Dual

Fact table:

Sales

Storage Mode:

DirectQuery

---

# 2.6 Composite Models

A composite model combines storage modes.

Example:

Import:

Product table

DirectQuery:

Sales transaction table

---

A composite model can contain:

* Import tables
* DirectQuery tables
* Dual tables

---

# PL-300 Rule

Composite model:

= Multiple storage modes in one model

Dual mode:

= A table that can switch behavior

They are related but not the same.

---

# 2.7 Power Query Overview

Power Query is Power BI's data preparation tool.

It is used before data enters the semantic model.

Power Query uses:

✅ M language

---

# Power Query Responsibilities

Use Power Query for:

* Cleaning data
* Transforming data
* Combining sources
* Removing unnecessary data

Examples:

* Remove duplicates
* Rename columns
* Change data types
* Split columns
* Merge tables
* Append tables

---

# Power Query Workflow

```id="89x9da"
Source Data

↓

Power Query Transformations

↓

Semantic Model

↓

DAX Calculations

↓

Report
```

---

# 2.8 Common Transformations

---

# Change Data Types

Example:

Text:

"100"

Convert to:

Number:

100

---

# Remove Columns

Remove unnecessary fields.

Benefits:

* Smaller model
* Better performance

---

# Remove Rows

Examples:

* Blank rows
* Errors
* Invalid records

---

# Split Columns

Example:

Full Name:

John Smith

↓

First Name:

John

Last Name:

Smith

---

# Pivot Columns

Convert rows into columns.

Example:

Before:

| Month | Sales |
| ----- | ----- |
| Jan   | 100   |
| Feb   | 200   |

After:

| Jan | Feb |
| --- | --- |
| 100 | 200 |

---

# Unpivot Columns

Convert columns into rows.

Common with Excel data.

---

# 2.9 Merge vs Append

Very common PL-300 topic.

---

# Merge

Purpose:

Combine tables horizontally.

Think:

SQL JOIN

Example:

Customer table:

| CustomerID | Name |
| ---------- | ---- |
| 1          | John |

Sales table:

| CustomerID | Amount |
| ---------- | ------ |
| 1          | 500    |

Merge result:

| CustomerID | Name | Amount |
| ---------- | ---- | ------ |
| 1          | John | 500    |

---

# Append

Purpose:

Combine tables vertically.

Think:

Stack rows.

Example:

January Sales

*

February Sales

=

All Sales

---

# Merge vs Append

| Merge                 | Append                   |
| --------------------- | ------------------------ |
| Combines columns      | Combines rows            |
| Requires matching key | Requires similar columns |
| Similar to JOIN       | Similar to UNION         |

---

# PL-300 Decision Rule

Need customer information added to sales?

✅ Merge

Need January + February sales combined?

✅ Append

---

# 2.10 Query Folding

Query folding is one of the most tested Power Query concepts.

---

# What Is Query Folding?

Query folding means Power Query pushes transformations back to the data source.

Example:

Power Query step:

Filter Sales where Year = 2026

Instead of:

```id="i1w5m5"
Load everything

↓

Filter in Power BI
```

Power BI sends:

```sql
SELECT *
FROM Sales
WHERE Year = 2026
```

to the database.

---

# Benefits of Query Folding

✅ Better performance
✅ Less data transferred
✅ Faster refreshes

---

# Sources That Support Folding

Common examples:

* SQL Server
* Azure SQL
* Databases

---

# Transformations That Often Break Folding

Examples:

* Certain custom functions
* Some complex transformations
* Python/R scripts

---

# PL-300 Rule

Query folding happens:

Before data reaches the semantic model.

---

# 2.11 Data Profiling

Power Query provides tools to understand data quality.

Tools include:

* Column quality
* Column distribution
* Column profile

---

# Used For:

Finding:

* Errors
* Null values
* Unexpected values
* Duplicates

---

# 2.12 Parameters

Parameters allow dynamic values in Power Query. Similare purpose as vraibles but for models.

Examples:

* File path
* Server name
* Date filters

---

# Example

Instead of:

```text
C:\Users\John\Sales.xlsx
```

Create:

```text
FilePath Parameter
```

Then change the parameter.

---

# Uses

Parameters help with:

* Reusable queries
* Environment changes
* Incremental refresh

---

# 2.13 Data Gateways

A gateway allows Power BI Service to access data stored on-premises.

Example:

```id="8u8zqk"
On-Prem SQL Server

↓

Gateway

↓

Power BI Service
```

---

# When Is Gateway Needed?

Usually:

On-premises data sources.

Examples:

* Local SQL Server
* File shares
* On-prem databases

---

# Cloud Sources

Usually do NOT require gateway.

Examples:

* Azure SQL
* SharePoint Online

---

# Gateway Types

## Personal Gateway

Used by individuals.

---

## Standard Gateway

Used by organizations.

Supports:

* Multiple users
* Shared connections
* Enterprise scenarios

---

# 2.14 Common PL-300 Exam Traps

---

## Trap 1

Connector and storage mode are the same.

❌ Incorrect

Connector = where data comes from

Storage mode = how Power BI uses it

---

## Trap 2

DirectQuery stores all data inside Power BI.

❌ Incorrect

DirectQuery queries the source.

---

## Trap 3

Merge adds rows.

❌ Incorrect

Merge adds columns.

---

## Trap 4

Append combines columns.

❌ Incorrect

Append combines rows.

---

## Trap 5

Query folding happens after loading data.

❌ Incorrect

Query folding happens during Power Query transformation.

---

## Trap 6

Gateway is needed for all data sources.

❌ Incorrect

Mostly needed for on-premises sources.

---

# Chapter 2 Practice Exam Questions

---

# Question 1

A company needs reports updated every few seconds from a database containing billions of rows.

Which storage mode should be used?

A. Import

B. DirectQuery

C. Dual

D. Cached

Correct Answer:

✅ B. DirectQuery

---

# Question 2

A developer needs to combine a Customer table with a Sales table using CustomerID.

Which transformation should be used?

A. Append

B. Merge

C. Pivot

D. Group By

Correct Answer:

✅ B. Merge

---

# Question 3

A company wants to combine January sales and February sales into one table.

Which transformation should be used?

A. Merge

B. Append

C. Relationship

D. Join

Correct Answer:

✅ B. Append

---

# Question 4

A Power Query transformation is pushed back to SQL Server for processing.

What feature is being used?

A. DAX

B. Query Folding

C. DirectQuery

D. Gateway

Correct Answer:

✅ B. Query Folding

---

# Question 5

A Power BI Service refresh needs to access an on-premises SQL Server.

What is required?

A. Bookmark

B. Gateway

C. Dashboard

D. App

Correct Answer:

✅ B. Gateway

---

# Question 6

A user wants to dynamically change a file path used by Power Query.

What should be created?

A. Measure

B. Parameter

C. Relationship

D. Bookmark

Correct Answer:

✅ B. Parameter

---

# Chapter 2 Summary

| Concept         | Purpose                         |
| --------------- | ------------------------------- |
| Connector       | Connect to data source          |
| Import          | Store data in model             |
| DirectQuery     | Query source directly           |
| Composite Model | Combine storage modes           |
| Dual Mode       | Flexible table storage          |
| Power Query     | Prepare data                    |
| DAX             | Calculate insights              |
| Merge           | Combine columns                 |
| Append          | Combine rows                    |
| Query Folding   | Push transformations to source  |
| Gateway         | Connect Service to on-prem data |

---

# Next Chapter

## Chapter 3 — Data Cleaning, Transformation, and Query Optimization

Topics:

* Advanced Power Query transformations
* Data types
* Handling errors
* Column profiling
* Merging strategies
* Query dependencies
* Parameters in practice
* Incremental refresh introduction
* PL-300 preparation scenarios
