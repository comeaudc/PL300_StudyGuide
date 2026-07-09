# Chapter 5 — DAX Fundamentals and Calculations

## Microsoft Power BI Data Analyst Associate (PL-300)

---

# Chapter Objectives

After completing this chapter, learners should understand:

* What DAX is
* When to use measures vs columns
* Row context
* Filter context
* Context transition
* Common DAX functions
* CALCULATE()
* Iterators
* Variables
* Time intelligence
* Common PL-300 DAX scenarios

---

# 5.1 What Is DAX?

DAX stands for:

**Data Analysis Expressions**

DAX is the formula language used in Power BI for:

* Measures
* Calculated columns
* Calculated tables

---

# DAX Purpose

DAX creates calculations that analyze data.

Examples:

* Total sales
* Profit margin
* Year-over-year growth
* Running totals
* Percent of total

---

# Where Is DAX Used?

DAX can create:

## Measures

Most common.

## Calculated Columns

Row-by-row calculations.

## Calculated Tables

New tables created from existing data.

---

# 5.2 Measures vs Calculated Columns

This is one of the most tested PL-300 topics.

---

# Calculated Column

A calculated column is evaluated during data refresh.

Example:

```DAX
Profit =
Sales[Revenue] - Sales[Cost]
```

The value is stored in the model.

---

# Measure

A measure is calculated when a visual requests it.

Example:

```DAX
Total Sales =
SUM(Sales[Amount])
```

---

# Comparison

| Calculated Column         | Measure                  |
| ------------------------- | ------------------------ |
| Calculated during refresh | Calculated at query time |
| Stored in model           | Not stored as values     |
| Row context               | Filter context           |
| Increases model size      | More efficient           |

---

# Decision Guide

Need:

Profit for every transaction?

✅ Calculated Column

Need:

Total sales by month?

✅ Measure

---

# 5.3 DAX Evaluation Context

Understanding context is essential.

DAX results depend on context.

Two important types:

1. Row context
2. Filter context

---

# 5.4 Row Context

Row context means:

> The current row being evaluated.

Common with:

* Calculated columns
* Iterators

Example:

Sales table:

| Quantity | Price |
| -------- | ----- |
| 5        | 10    |

Calculated column:

```DAX
Revenue =
Sales[Quantity] * Sales[Price]
```

Power BI evaluates each row:

Row 1:

5 × 10 = 50

---

# 5.5 Filter Context

Filter context means:

> The filters currently applied to a calculation.

Examples:

* Slicers
* Visual filters
* Page filters
* Report filters

---

Example:

Measure:

```DAX
Total Sales =
SUM(Sales[Amount])
```

A visual filtered to:

Region = East

returns:

Only East sales.

---

# 5.6 Context Example

Measure:

```DAX
Total Sales =
SUM(Sales[Amount])
```

A card visual:

No filters:

$1,000,000

A table:

Region East:

$250,000

Region West:

$300,000

Same measure.

Different filter context.

---

# 5.7 CALCULATE()

CALCULATE is one of the most important DAX functions.

Purpose:

> Changes filter context.

Syntax:

```DAX
CALCULATE(
    Expression,
    Filter
)
```

---

Example:

Normal:

```DAX
Total Sales =
SUM(Sales[Amount])
```

Only calculate sales for 2026:

```DAX
Sales 2026 =
CALCULATE(
    SUM(Sales[Amount]),
    Sales[Year] = 2026
)
```

---

# Why CALCULATE Matters

It allows:

* Custom filtering
* Time intelligence
* Comparisons
* Advanced calculations

---

# 5.8 Context Transition

CALCULATE can transform:

Row context

into

Filter context

This is called:

Context transition

---

PL-300 Level:

Know that:

CALCULATE changes evaluation behavior.

---

# 5.9 Common Aggregation Functions

---

# SUM()

Adds values.

Example:

```DAX
Total Sales =
SUM(Sales[Amount])
```

---

# COUNT()

Counts numeric values.

---

# COUNTROWS()

Counts rows in a table.

Example:

```DAX
Order Count =
COUNTROWS(Sales)
```

---

# DISTINCTCOUNT()

Counts unique values.

Example:

```DAX
Customers =
DISTINCTCOUNT(Customer[CustomerID])
```

---

# SUM vs COUNTROWS

Sales Amount:

Use:

✅ SUM

Number of transactions:

Use:

✅ COUNTROWS

---

# 5.10 Iterators (X Functions)

Iterator functions evaluate row-by-row.

Common examples:

* SUMX()
* AVERAGEX()
* COUNTX()

---

# SUMX()

Example:

A table has:

Quantity

Price

Need:

Quantity × Price

```DAX
Revenue =
SUMX(
Sales,
Sales[Quantity] * Sales[Price]
)
```

---

# SUM vs SUMX

SUM:

Adds one column.

SUMX:

Calculates an expression for every row.

---

# 5.11 ALL()

ALL removes filters.

Example:

```DAX
Total Company Sales =
CALCULATE(
    SUM(Sales[Amount]),
    ALL(Sales)
)
```

Used for:

* Percent of total
* Comparisons

---

# Example

Region Sales:

East:

$200

West:

$300

Total:

$500

Percent:

East:

200 / 500

---

# 5.12 REMOVEFILTERS()

Similar purpose:

Removes filters.

Example:

```DAX
Total Sales =
CALCULATE(
SUM(Sales[Amount]),
REMOVEFILTERS(Product)
)
```

---

# 5.13 VALUES()

VALUES returns unique values from a column.

Example:

```DAX
VALUES(Customer[Region])
```

Returns:

East

West

North

---

# VALUES vs DISTINCT

Both return unique values.

Important PL-300 concept:

VALUES can include a blank value caused by relationship issues.

---

# 5.14 Variables

Variables improve readability.

Example:

Without variable:

```DAX
Profit Margin =
DIVIDE(
SUM(Sales[Profit]),
SUM(Sales[Revenue])
)
```

With variable:

```DAX
Profit Margin =
VAR Profit =
SUM(Sales[Profit])

VAR Revenue =
SUM(Sales[Revenue])

RETURN
DIVIDE(Profit,Revenue)
```

---

# Benefits:

* Easier debugging
* Better readability
* Sometimes better performance

---

# 5.15 DIVIDE()

Preferred over division operator.

Avoid:

```DAX
Sales / Quantity
```

Use:

```DAX
DIVIDE(
Sales,
Quantity
)
```

---

# Why?

Handles divide-by-zero safely.

---

# 5.16 Time Intelligence

Time intelligence analyzes data over time.

Examples:

* Year-to-date
* Previous year
* Month-over-month

---

# Requirements

Need:

✅ Proper Date Table

The table should:

* Contain unique dates
* Cover the date range
* Be marked as a date table

---

# Common Functions

## TOTALYTD()

Year-to-date.

---

## SAMEPERIODLASTYEAR()

Previous year comparison.

Example:

2026 Sales

vs

2025 Sales

---

## DATEADD()

Shift dates.

Example:

Previous month.

---

# 5.17 Calculated Tables

Calculated tables create new tables using DAX.

Example:

```DAX
Calendar =
CALENDAR(
DATE(2025,1,1),
DATE(2026,12,31)
)
```

---

# Use Cases:

* Date tables
* Helper tables
* Analysis tables

---

# 5.18 Common PL-300 DAX Traps

---

## Trap 1

Measures are calculated during refresh.

❌ Incorrect

Measures calculate when queried.

---

## Trap 2

Calculated columns respond to slicers.

❌ Incorrect

They are already calculated.

---

## Trap 3

SUMX and SUM are identical.

❌ Incorrect

SUMX evaluates an expression row-by-row.

---

## Trap 4

CALCULATE adds values together.

❌ Incorrect

CALCULATE modifies filter context.

---

## Trap 5

Time intelligence works without a date table.

❌ Incorrect

A proper date table is required.

---

# Chapter 5 Practice Questions

---

# Question 1

A user needs total sales that changes when users select different regions.

What should be created?

A. Calculated column

B. Measure

C. Power Query column

D. Calculated table

Correct Answer:

✅ B. Measure

---

# Question 2

A calculated column calculates:

Quantity × Price

What context is being used?

A. Filter context

B. Row context

C. Query context

D. Security context

Correct Answer:

✅ B. Row context

---

# Question 3

A measure must calculate sales only for the current year.

Which function should be used?

A. SUMX

B. CALCULATE

C. VALUES

D. DISTINCTCOUNT

Correct Answer:

✅ B. CALCULATE

---

# Question 4

A calculation requires removing all filters to calculate a company total.

Which function should be used?

A. ALL

B. SUM

C. COUNT

D. RELATED

Correct Answer:

✅ A. ALL

---

# Question 5

A company needs year-over-year sales comparisons.

What must exist?

A. Gateway

B. Date table

C. Dashboard

D. Bookmark

Correct Answer:

✅ B. Date table

---

# Question 6

A calculation requires multiplying quantity by price for each transaction before summing.

Which function should be used?

A. SUM

B. SUMX

C. COUNTROWS

D. VALUES

Correct Answer:

✅ B. SUMX

---

# Chapter 5 Summary

| Concept           | Purpose                 |
| ----------------- | ----------------------- |
| DAX               | Create calculations     |
| Measure           | Dynamic calculations    |
| Calculated Column | Row-level stored values |
| Row Context       | Current row             |
| Filter Context    | Applied filters         |
| CALCULATE         | Modify filters          |
| SUMX              | Row-by-row calculations |
| COUNTROWS         | Count records           |
| DISTINCTCOUNT     | Count unique values     |
| ALL               | Remove filters          |
| VALUES            | Return unique values    |
| Variables         | Improve formulas        |
| Time Intelligence | Analyze dates           |

---

# Next Chapter

## Chapter 6 — Visualizations and Report Design

Topics:

* Choosing visuals
* Slicers
* Filters
* Drill down
* Drillthrough
* Tooltips
* Bookmarks
* Sync slicers
* Conditional formatting
* Key Influencers
* Decomposition Tree
* PL-300 visual scenarios
