# Chapter 3 — Data Preparation and Power Query Transformations

## Microsoft Power BI Data Analyst Associate (PL-300)

---

# Chapter Objectives

After completing this chapter, learners should understand:

* The purpose of data preparation
* Power Query transformation techniques
* Data profiling tools
* Cleaning poor-quality data
* Managing data types
* Combining and restructuring data
* Query dependencies
* Reference vs Duplicate queries
* Transformation best practices
* How preparation affects performance

---

# 3.1 Why Data Preparation Matters

Raw data is rarely ready for analysis.

Common problems:

* Incorrect data types
* Missing values
* Duplicate records
* Inconsistent formatting
* Extra columns
* Poor naming conventions

Power Query prepares data before it enters the semantic model.

---

# Data Preparation Flow

```id="8h7b4k"
Raw Data

↓

Power Query

↓

Clean Data

↓

Semantic Model

↓

Reports
```

---

# PL-300 Rule

If the problem exists in the source data:

Use:

✅ Power Query

Not:

❌ DAX

---

# Example

Bad Data:

| Customer   | Sales |
| ---------- | ----- |
| john smith | 500   |
| John Smith | 500   |
| JOHN SMITH | 500   |

Solution:

Power Query:

* Standardize text
* Remove duplicates

---

# 3.2 Power Query Editor Overview

Power Query contains:

## Queries Pane

Shows all queries.

---

## Data Preview

Shows transformation results.

---

## Applied Steps

Records every transformation.

Example:

```id="3x5e7u"
Source

↓

Changed Type

↓

Removed Columns

↓

Filtered Rows
```

---

# Applied Steps

Each transformation creates an M step.

Benefits:

* Repeatable process
* Auditable transformations
* Easy troubleshooting

---

# PL-300 Scenario

An analyst needs to see what transformations were applied.

Where should they look?

Correct:

✅ Applied Steps

---

# 3.3 Data Profiling Tools

Power Query provides tools to understand data quality.

Enable:

View → Data Preview

---

# Column Quality

Shows:

* Valid values
* Errors
* Empty values

Example:

| Column | Valid | Error |
| ------ | ----- | ----- |
| Sales  | 98%   | 2%    |

---

# Column Distribution

Shows:

* Unique values
* Distinct values
* Frequency

Useful for:

* Finding duplicates
* Understanding categories

---

# Column Profile

Shows:

* Statistics
* Value distribution
* Min/max values

---

# PL-300 Scenario

An analyst wants to identify columns containing unexpected null values.

Use:

✅ Column Quality

---

# 3.4 Managing Data Types

Correct data types are critical.

Common types:

* Text
* Whole Number
* Decimal Number
* Date
* Date/Time
* Boolean

---

# Why Data Types Matter

Incorrect data types cause:

* Incorrect calculations
* Relationship problems
* Poor performance

---

Example:

Sales Amount:

Incorrect:

Text

"500"

Correct:

Number

500

---

# Automatic Data Type Detection

Power Query often automatically assigns types.

However:

Always verify.

---

# PL-300 Trap

Automatic detection does not guarantee correctness.

---

# 3.5 Removing Unnecessary Data

Reducing data improves performance.

Remove:

* Unused columns
* Historical data not needed
* Duplicate information

---

# Remove Columns

Example:

Source:

| Customer | Address | Phone | Notes |
| -------- | ------- | ----- | ----- |

Analysis only needs:

Customer

Remove:

* Address
* Phone
* Notes

---

# Remove Rows

Examples:

Remove:

* Blank records
* Test records
* Invalid transactions

---

# 3.6 Handling Errors

Power Query can identify errors.

Examples:

* Invalid dates
* Failed conversions
* Missing values

---

# Error Handling Options

## Remove Errors

Deletes rows containing errors.

Use when:

Errors are invalid records.

---

## Replace Errors

Replaces errors with a value.

Example:

Error:

Sales Amount

Replace:

0

---

## Keep Errors

Useful for investigation.

---

# PL-300 Scenario

A company has invalid test transactions that should not appear in reports.

Best solution:

✅ Remove error rows in Power Query

---

# 3.7 Replace Values

Replace Values changes existing values.

Example:

Before:

| State |
| ----- |
| Mass  |
| MA    |

After:

| State         |
| ------------- |
| Massachusetts |

---

# Common Uses

* Standardizing categories
* Fixing spelling mistakes
* Cleaning inconsistent labels

---

# 3.8 Conditional Columns

Conditional columns create logic-based columns.

Example:

Sales Amount:

If:

> 10000

Then:

"High Value"

Else:

"Standard"

---

# Conditional Column vs DAX

Use Conditional Column when:

The value is part of data preparation.

Use DAX when:

The value depends on analysis context.

---

# 3.9 Group By

Group By summarizes data.

Example:

Sales table:

| Region | Sales |
| ------ | ----- |
| East   | 100   |
| East   | 200   |

Group By Region:

| Region | Total |
| ------ | ----- |
| East   | 300   |

---

# Uses:

* Aggregations
* Summaries
* Removing duplicates

---

# 3.10 Pivot and Unpivot

---

# Pivot

Turns rows into columns.

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

# Unpivot

Turns columns into rows.

Common Excel scenario:

Before:

| Product | Jan | Feb |
| ------- | --- | --- |
| A       | 100 | 200 |

After:

| Product | Month | Sales |
| ------- | ----- | ----- |
| A       | Jan   | 100   |
| A       | Feb   | 200   |

---

# PL-300 Rule

Unpivot is frequently used to normalize spreadsheet data.

---

# 3.11 Reference vs Duplicate Queries

Very common exam concept.

---

# Duplicate Query

Creates an independent copy.

Changes to original:

❌ Do not affect duplicate

---

# Reference Query

Creates a new query based on another query.

Changes to original:

✅ Flow into reference

---

# Example

Main Query:

Sales Raw Data

Reference:

Sales Summary

If Sales Raw Data changes:

Sales Summary updates.

---

# Reference vs Duplicate

| Reference               | Duplicate                       |
| ----------------------- | ------------------------------- |
| Depends on original     | Independent copy                |
| Good for reusable logic | Good for separate modifications |

---

# 3.12 Query Dependencies

Query Dependencies show relationships between queries.

Example:

```id="x94jrh"
Sales Raw

↓

Sales Clean

↓

Sales Summary
```

---

# Used For:

* Understanding transformations
* Troubleshooting
* Managing complex models

---

# 3.13 Transformation Order Best Practices

A common optimization strategy:

Recommended order:

1. Remove unnecessary rows
2. Remove unnecessary columns
3. Filter data
4. Change data types
5. Transform values
6. Merge/Append
7. Load data

---

# Why?

Reduce data early.

Example:

Better:

Remove 1 million rows before transformations.

Worse:

Transform 1 million unnecessary rows.

---

# 3.14 Parameters in Power Query

Parameters store reusable values.

Examples:

* File paths
* Server names
* Date filters

---

Example:

Instead of:

```text
C:\Sales\2026.xlsx
```

Use:

```text
FilePath Parameter
```

---

# Benefits:

* Easier maintenance
* Environment switching
* Reusable queries

---

# 3.15 Incremental Refresh Introduction

Incremental refresh improves refresh performance.

Instead of refreshing:

All historical data

It refreshes:

Only recent data.

Example:

Historical:

2015-2025

Refresh:

Last 30 days

---

# Requires:

A date/time column.

Uses:

RangeStart

RangeEnd

parameters.

---

# PL-300 Scenario

A company has 10 years of sales data but only yesterday's data changes.

Use:

✅ Incremental Refresh

---

# 3.16 Common PL-300 Exam Traps

---

## Trap 1

Clean data using DAX.

❌ Incorrect

Use Power Query.

---

## Trap 2

Reference creates an independent copy.

❌ Incorrect

Duplicate creates an independent copy.

---

## Trap 3

Merge combines rows.

❌ Incorrect

Merge combines columns.

---

## Trap 4

Unpivot makes data wider.

❌ Incorrect

Unpivot makes data taller.

---

## Trap 5

Remove unused columns after loading.

❌ Incorrect

Remove them before loading.

---

# Chapter 3 Practice Questions

---

# Question 1

An analyst needs to identify columns containing missing values before cleaning.

Which feature should be used?

A. Column Quality

B. DAX Measure

C. Relationship View

D. Dashboard

Correct Answer:

✅ A. Column Quality

---

# Question 2

A table contains monthly sales stored as separate columns.

What transformation should be used before creating a model?

A. Pivot

B. Unpivot

C. Merge

D. Append

Correct Answer:

✅ B. Unpivot

---

# Question 3

An analyst creates a new query based on another query and wants future changes to flow through.

Which option should they use?

A. Duplicate

B. Reference

C. Copy

D. Export

Correct Answer:

✅ B. Reference

---

# Question 4

A company wants to reduce refresh time by only processing recent transactions.

What should be implemented?

A. RLS

B. Incremental Refresh

C. Bookmark

D. Dashboard

Correct Answer:

✅ B. Incremental Refresh

---

# Question 5

A dataset contains thousands of unused columns.

What should be done?

A. Hide columns in the report

B. Remove columns in Power Query

C. Create measures

D. Use filters

Correct Answer:

✅ B. Remove columns in Power Query

---

# Chapter 3 Summary

| Concept             | Purpose                 |
| ------------------- | ----------------------- |
| Power Query         | Prepare data            |
| Data Profiling      | Understand quality      |
| Data Types          | Ensure correct behavior |
| Replace Values      | Standardize values      |
| Group By            | Aggregate data          |
| Pivot               | Rows → Columns          |
| Unpivot             | Columns → Rows          |
| Merge               | Combine columns         |
| Append              | Combine rows            |
| Reference           | Reusable query          |
| Duplicate           | Independent copy        |
| Parameters          | Dynamic values          |
| Incremental Refresh | Faster refresh          |

---

# Next Chapter

## Chapter 4 — Data Modeling Fundamentals

Topics:

* Star schema
* Fact tables
* Dimension tables
* Relationships
* Cardinality
* Filter direction
* Date tables
* Many-to-many relationships
* Model optimization
* PL-300 modeling scenarios
