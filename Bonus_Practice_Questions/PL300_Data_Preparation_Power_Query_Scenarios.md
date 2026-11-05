# PL-300 Scenario Practice: Data Preparation, Power Query, and Data Quality

**Format:** 10 scenario-based multiple-choice questions  
**Level:** Foundational to lower-intermediate  
**Focus:** Data preparation, Power Query transformations, profiling, data quality, data types, combining/restructuring data, query dependencies, Reference vs. Duplicate, best practices, and performance.

These are original practice questions aligned to the general themes in the Microsoft PL-300 study guide, not official exam questions.

---

## Question 1 — The Purpose of Data Preparation

A retail company receives monthly sales files from several branches. The files use different column names, some dates are stored as text, and product categories are inconsistent. Analysts want reliable reports comparing sales across branches.

What should the analyst do first?

A. Create DAX measures to calculate total sales  
B. Prepare and standardize the data in Power Query before building the model  
C. Create a dashboard and correct issues as users report them  
D. Add a separate report page for each branch

**Correct answer: B. Prepare and standardize the data in Power Query before building the model.**

**Explanation:** Data preparation makes source data consistent and usable for analysis. Standardizing column names, data types, and category values helps prevent inaccurate comparisons and reduces repeated cleanup later.

---

## Question 2 — Power Query Transformation Techniques

A source table contains one row per product and separate columns for `Jan`, `Feb`, and `Mar` sales. The analyst needs a table with one row per product per month, using columns named `Product`, `Month`, and `Sales`.

Which transformation should the analyst use?

A. Merge Queries  
B. Append Queries  
C. Unpivot the month columns  
D. Group By

**Correct answer: C. Unpivot the month columns.**

**Explanation:** Unpivot converts multiple month columns into attribute-value rows, making the data easier to filter, chart, and analyze over time. Merge joins columns from related tables; append stacks rows from tables.

---

## Question 3 — Data Profiling Tools

An analyst suspects that a `CustomerEmail` column contains missing values and invalid entries. They want a quick visual summary of valid values, errors, and empty values for the column.

Which Power Query data-profiling tool is the best fit?

A. Column Quality  
B. Column Distribution  
C. Column Profile  
D. Query Dependencies

**Correct answer: A. Column Quality.**

**Explanation:** Column Quality summarizes the percentage of valid, error, and empty values. Column Distribution focuses on value frequency and distinct/unique values, while Column Profile provides more detailed statistics for a selected column.

---

## Question 4 — Cleaning Poor-Quality Data

A `Region` column contains values such as `North`, `north`, `NORTH `, and ` North`. These values should be treated as the same region in reports.

What is the most appropriate preparation step?

A. Convert the column to a whole number  
B. Trim whitespace and standardize capitalization  
C. Remove every row containing a lowercase value  
D. Replace the entire column with null values

**Correct answer: B. Trim whitespace and standardize capitalization.**

**Explanation:** Leading/trailing spaces and inconsistent capitalization can create duplicate categories. Clean the text consistently so grouping and filtering work as expected. Confirm the intended standard before replacing values.

---

## Question 5 — Managing Data Types

A CSV file contains an `OrderDate` column with values such as `10/11/2026`. Power Query currently identifies the column as Text, and the report must support date filtering and time-based analysis. The source format is known to be month/day/year.

What should the analyst do?

A. Leave the column as Text and sort it alphabetically  
B. Convert the column to Date using the appropriate locale  
C. Convert the column to Whole Number  
D. Create a calculated column in DAX that concatenates the text

**Correct answer: B. Convert the column to Date using the appropriate locale.**

**Explanation:** A correct Date type enables date filtering, relationships to a date table, and time-based calculations. When dates are ambiguous or use a locale-specific format, set the appropriate locale to avoid interpreting month and day incorrectly.

---

## Question 6 — Combining Data

A company stores January sales and February sales in two tables with the same column structure. The analyst wants one table containing all rows from both months.

Which action should the analyst take?

A. Merge the queries using `ProductID`  
B. Append the queries  
C. Create a relationship between the two tables  
D. Use Group By on each table separately

**Correct answer: B. Append the queries.**

**Explanation:** Append stacks rows from one table beneath the rows of another. Merge combines columns by matching rows based on one or more key columns. Matching column names and compatible data types make appending more predictable.

---

## Question 7 — Query Dependencies

An analyst has a `RawSales` query, a `CleanSales` query that references it, and a `MonthlySales` query built from `CleanSales`. They need to understand which queries depend on one another before changing a transformation.

Which Power Query feature should they inspect?

A. Column Distribution  
B. Query Dependencies  
C. Manage Parameters  
D. Data Category

**Correct answer: B. Query Dependencies.**

**Explanation:** Query Dependencies displays how queries and data sources relate to one another. Reviewing the dependency chain helps the analyst understand which downstream queries may be affected by a change.

---

## Question 8 — Reference vs. Duplicate Queries

An analyst has a cleaned `Sales_Base` query. They need a second query that starts from the prepared result and applies a different filter, while keeping the transformation logic connected to the base query so changes to the base can flow downstream.

What should the analyst choose?

A. Duplicate the `Sales_Base` query  
B. Reference the `Sales_Base` query  
C. Export the base query to CSV and import it again  
D. Create a relationship to the base query

**Correct answer: B. Reference the `Sales_Base` query.**

**Explanation:** A Reference query uses the result of the original query as its starting point, so upstream changes can flow into the referenced query. A Duplicate creates a separate copy of the query's existing steps; later edits to the original query's steps do not automatically become edits to the duplicate's steps.

---

## Question 9 — Transformation Best Practices

A data source has 30 columns, but the report only needs 8. Several columns contain large text fields that are not used in the model. The analyst wants to reduce unnecessary processing and model size.

What is the best practice?

A. Keep all columns in case they might be useful later  
B. Remove unnecessary columns early in the preparation process  
C. Convert every column to Text  
D. Load the full source and hide unused columns only in the report

**Correct answer: B. Remove unnecessary columns early in the preparation process.**

**Explanation:** Removing unneeded columns reduces the amount of data carried through later transformations and can reduce model size. When working with foldable sources, early filters and column selection may also be pushed back to the source through query folding.

---

## Question 10 — How Preparation Affects Performance

A Power Query query connects to a supported relational database. It applies several transformations, but the analyst notices that query folding stops before a large filter step. The filter could otherwise reduce millions of source rows to a small subset.

What should the analyst investigate first?

A. Whether the filter and preceding transformations can be rearranged or rewritten to preserve query folding  
B. Whether to replace all Power Query steps with report visuals  
C. Whether to add more columns to the source query  
D. Whether to turn every column into a calculated column in DAX

**Correct answer: A. Whether the filter and preceding transformations can be rearranged or rewritten to preserve query folding.**

**Explanation:** Query folding allows supported transformations to be translated into a query executed by the source system. Preserving folding—especially for selective filters—can reduce data transferred and improve refresh performance. Not every connector or transformation supports folding, so verify the behavior for the actual source.

---

## Quick Review

| Topic | Remember |
|---|---|
| Purpose of preparation | Make data consistent, reliable, and ready for modeling and analysis |
| Transformation techniques | Use the right operation: filter, replace, split, merge, append, pivot, or unpivot |
| Column Quality | Shows valid, error, and empty values |
| Cleaning data | Standardize whitespace, capitalization, categories, and missing/error values carefully |
| Data types | Assign correct types; use locale when parsing ambiguous dates/numbers |
| Combining data | Append stacks rows; Merge joins columns based on matching keys |
| Query dependencies | Shows relationships and downstream effects among queries |
| Reference vs. Duplicate | Reference starts from another query's result; Duplicate copies its existing query steps |
| Best practices | Remove unused columns, filter appropriately, and keep transformations understandable |
| Performance | Preserve query folding where possible and avoid carrying unnecessary data |

## Exam Tips

- **Append = add rows; Merge = add columns by matching keys.**
- **Column Quality = valid/error/empty; Column Distribution = frequency and distinct/unique values; Column Profile = detailed statistics.**
- **Reference** is useful for branching from a shared preparation query. **Duplicate** gives you a separate copy of the existing steps.
- Correct data types matter for sorting, filtering, relationships, and calculations.
- For supported sources, query folding can improve refresh efficiency by having the source perform eligible work.
