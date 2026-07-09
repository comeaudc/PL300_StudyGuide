# Chapter 4 — Data Modeling Fundamentals

## Microsoft Power BI Data Analyst Associate (PL-300)

---

# Chapter Objectives

After completing this chapter, learners should understand:

* Why data modeling is important
* Star schema design
* Fact and dimension tables
* Relationships
* Cardinality
* Cross-filter direction
* Active and inactive relationships
* Date tables
* Measures vs calculated columns
* Hierarchies
* Model optimization
* Common PL-300 modeling scenarios

---

# 4.1 What Is Data Modeling?

Data modeling is the process of organizing data so Power BI can efficiently analyze it.

A good model:

* Improves performance
* Simplifies DAX
* Makes reports easier to build
* Prevents incorrect calculations

---

# Power BI Modeling Layer

```id="0sm9n7"
Data Sources

↓

Power Query

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

# 4.2 Star Schema

Star schema is Microsoft's recommended modeling approach.

A star schema contains:

* Fact tables
* Dimension tables

---

# Example

```id="l3s9z2"
        Customer
            |
            |
Product --- Sales --- Date
            |
            |
        Store
```

The fact table is in the center.

Dimensions surround it.

---

# Why Use Star Schema?

Benefits:

✅ Better performance
✅ Easier DAX
✅ Cleaner relationships
✅ Better user experience

---

# 4.3 Fact Tables

Fact tables contain measurable business events.

Examples:

* Sales transactions
* Orders
* Inventory movements
* Website clicks

Usually contain:

* Foreign keys
* Numeric values

Example:

Sales Fact:

| DateKey | ProductKey | CustomerKey | SalesAmount |
| ------- | ---------- | ----------- | ----------- |
| 1       | 10         | 50          | 250         |

---

# Fact Table Characteristics

Usually:

* Many rows
* Contains measurements
* Connects to dimensions

---

# 4.4 Dimension Tables

Dimension tables describe business entities.

Examples:

* Customers
* Products
* Dates
* Locations

Example:

Customer Dimension:

| CustomerKey | CustomerName | Region |
| ----------- | ------------ | ------ |
| 50          | John Smith   | East   |

---

# Dimension Table Characteristics

Usually:

* Fewer rows
* Contains descriptive information
* Used for filtering

---

# Fact vs Dimension

| Fact Table   | Dimension Table  |
| ------------ | ---------------- |
| Events       | Descriptions     |
| Numbers      | Categories       |
| Many rows    | Fewer rows       |
| Sales amount | Product name     |
| Transactions | Customer details |

---

# PL-300 Scenario

A company has:

Sales transactions

and

Customer information

Where should customer names be stored?

Correct:

✅ Customer dimension table

---

# 4.5 Relationships

Relationships connect tables together.

Example:

```id="2ms0zq"
Customer

CustomerID

    ↓

Sales

CustomerID
```

---

# Why Relationships Matter

They allow:

* Filtering
* Aggregation
* Data analysis

---

# 4.6 Relationship Cardinality

Cardinality describes how many rows match between tables.

---

# One-to-Many (1:*)

Most common relationship.

Example:

One customer:

↓

Many sales transactions

```id="m3l4pz"
Customer (1)

        ↓

Sales (*)
```

---

# Many-to-One (*:1)

Same relationship viewed from the opposite direction.

---

# One-to-One (1:1)

Rare.

Example:

Employee table:

Employee ID

↓

Employee Details

---

# Many-to-Many (*:*)

Multiple records can match on both sides.

Example:

Students and Courses.

A student can have many courses.

A course can have many students.

---

# PL-300 Warning

Many-to-many relationships can create:

* Ambiguous filtering
* Unexpected calculations

Use carefully.

---

# 4.7 Cross-Filter Direction

Cross-filter direction determines how filters move.

---

# Single Direction

Recommended default.

Example:

```id="v3wv1h"
Customer

↓

Sales
```

Customer filters Sales.

---

# Both Directions

Filters move both ways.

Example:

```id="r4r6nk"
Customer

↔

Sales
```

---

# When Use Both?

Only when needed.

Common scenarios:

* Many-to-many relationships
* Complex models

---

# PL-300 Trap

Bidirectional filtering always improves models.

❌ Incorrect

It can create ambiguity and performance issues.

---

# 4.8 Active vs Inactive Relationships

A model can have multiple relationships between tables.

Example:

Sales table:

Order Date

Ship Date

Both connect to:

Date table

---

Only one can be active.

Example:

Active:

Order Date

Inactive:

Ship Date

---

# Using Inactive Relationships

DAX can activate them.

Example:

```DAX id="s6m21h"
USERELATIONSHIP()
```

---

# 4.9 Date Tables

Date tables are essential for time intelligence.

Examples:

* Year
* Quarter
* Month
* Day

---

# Good Date Table

Contains:

| Date | Year | Month | Quarter |
| ---- | ---- | ----- | ------- |

---

# Date Table Requirements

Should:

✅ Have unique dates
✅ Cover entire analysis period
✅ Be marked as a date table

---

# Why Use Date Tables?

Required for:

* Year-to-date
* Previous year
* Month comparisons

---

# PL-300 Scenario

A user wants to create year-over-year sales analysis.

What should be created?

Correct:

✅ Date table

---

# 4.10 Measures vs Calculated Columns

This is one of the most tested PL-300 concepts.

---

# Calculated Column

Calculated during data refresh.

Stored in the model.

Example:

```DAX
Profit =
Sales[Revenue] - Sales[Cost]
```

---

# Measure

Calculated when the report is queried.

Example:

```DAX
Total Sales =
SUM(Sales[Amount])
```

---

# Calculated Column vs Measure

| Calculated Column     | Measure                |
| --------------------- | ---------------------- |
| Stored in model       | Calculated dynamically |
| Row-level calculation | Aggregation            |
| Uses row context      | Uses filter context    |
| Increases model size  | More efficient         |

---

# Decision Guide

Need:

Profit for each row?

✅ Calculated Column

Need:

Total sales by region?

✅ Measure

---

# 4.11 Implicit vs Explicit Measures

---

# Implicit Measure

Automatically created.

Example:

Dragging Sales Amount into a visual.

Power BI creates:

SUM(Sales Amount)

---

# Explicit Measure

Created manually using DAX.

Example:

```DAX
Total Sales =
SUM(Sales[Amount])
```

---

# PL-300 Best Practice

Use:

✅ Explicit measures

Because they:

* Are reusable
* Are easier to maintain
* Provide better control

---

# 4.12 Hierarchies

Hierarchies allow drill-down analysis.

Example:

Date hierarchy:

```id="n8c5x2"
Year

↓

Quarter

↓

Month

↓

Day
```

---

# Common Hierarchies

* Date
* Geography
* Product

---

# 4.13 Model Optimization

Good models:

* Remove unnecessary columns
* Use star schema
* Avoid unnecessary relationships
* Prefer measures
* Reduce cardinality

---

# High Cardinality Examples

Bad:

Transaction ID

Customer Email

Good:

Country

Category

---

# Why?

High cardinality increases memory usage.

---

# 4.14 Common PL-300 Exam Traps

---

## Trap 1

Fact tables contain descriptions.

❌ Incorrect

Dimensions contain descriptions.

---

## Trap 2

Calculated columns are always better than measures.

❌ Incorrect

Measures are preferred for aggregations.

---

## Trap 3

Many-to-many relationships should always be used.

❌ Incorrect

Use carefully.

---

## Trap 4

Bidirectional filtering improves every model.

❌ Incorrect

Can create ambiguity.

---

## Trap 5

A date column is enough for time intelligence.

❌ Incorrect

A proper date table is recommended.

---

# Chapter 4 Practice Questions

---

# Question 1

A sales model contains:

* Sales transactions
* Customer information
* Product information

What schema should be used?

A. Snowflake only

B. Star schema

C. Flat table

D. Many-to-many

Correct Answer:

✅ B. Star schema

---

# Question 2

A customer can have many sales transactions.

What relationship should be created?

A. One-to-one

B. One-to-many

C. Many-to-many

D. No relationship

Correct Answer:

✅ B. One-to-many

---

# Question 3

An analyst needs total sales by region.

What should they create?

A. Calculated column

B. Measure

C. Duplicate table

D. Parameter

Correct Answer:

✅ B. Measure

---

# Question 4

A report requires sales comparison between Order Date and Ship Date.

What should be used?

A. Duplicate fact table

B. USERELATIONSHIP()

C. Many-to-many

D. Bidirectional filtering

Correct Answer:

✅ B. USERELATIONSHIP()

---

# Question 5

A model contains a date field but year-over-year calculations do not work correctly.

What should be added?

A. Dashboard

B. Date table

C. Gateway

D. Bookmark

Correct Answer:

✅ B. Date table

---

# Chapter 4 Summary

| Concept           | Purpose                        |
| ----------------- | ------------------------------ |
| Star Schema       | Recommended model design       |
| Fact Table        | Stores events and measurements |
| Dimension Table   | Stores descriptions            |
| Relationship      | Connects tables                |
| Cardinality       | Defines matching rows          |
| Single Direction  | Recommended filtering          |
| Date Table        | Enables time intelligence      |
| Measure           | Dynamic calculation            |
| Calculated Column | Row-level calculation          |
| Hierarchy         | Drill-down analysis            |
| USERELATIONSHIP   | Use inactive relationships     |

---

# Next Chapter

## Chapter 5 — DAX Fundamentals and Calculations

Topics:

* Measures
* Calculated columns
* Row context
* Filter context
* CALCULATE()
* FILTER()
* ALL()
* SUMX()
* COUNTROWS()
* Time intelligence
* DAX evaluation scenarios
