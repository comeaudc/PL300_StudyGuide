
# PL-300 Expert Practice Questions (Set 1)

## Question 1 – Auto Date/Time
A Microsoft Fabric semantic model contains 10 fact tables. Each fact table has OrderDate, ShipDate, and InvoiceDate. Auto Date/Time is enabled. Users report the semantic model is much larger than expected.

What should you do?

A. Create a separate Date table for each fact table.
B. Disable Auto Date/Time and create one marked Date table used throughout the model.
C. Convert all Date columns to Text.
D. Remove all relationships to Date columns.

**Answer:** B

**Explanation:** Auto Date/Time creates a hidden date table for every eligible date column. One shared, marked Date table reduces model size and is Microsoft's recommended practice.

---

## Question 2 – High Cardinality

A Sales table contains a GUID column with 150 million unique values. The column is never used in reports or relationships.

A. Hide the column.
B. Convert it to Text.
C. Remove the column during data preparation.
D. Create a hierarchy.

**Answer:** C

**Explanation:** High-cardinality columns consume significant memory. Removing them reduces semantic model size. Hiding a column does not reduce storage.

---

## Question 3 – Query Folding

Query folding stops after adding a custom M function.

A. Rewrite the logic so it executes in SQL.
B. Create a calculated column.
C. Switch to Live Connection.
D. Enable Auto Date/Time.

**Answer:** A

**Explanation:** Preserving query folding pushes work to the source system and improves refresh performance.

---

## Question 4 – Workspace Roles vs RLS

Sophia should only see East region sales. Ryan should only view reports. Emma should edit reports.

A. Emma=Member, Ryan=Viewer, Sophia=Viewer + Dynamic RLS
B. Emma=Admin, Ryan=Member, Sophia=Viewer
C. Everyone=Viewer
D. Create three workspaces

**Answer:** A

**Explanation:** Workspace roles control content permissions; Dynamic RLS controls which rows users can see.

---

## Question 5 – Storage Modes

A 900-million-row Sales table uses DirectQuery. Users primarily analyze monthly totals.

A. Import the Sales table.
B. Create Import aggregation tables.
C. Duplicate the Sales table.
D. Convert Product to Text.

**Answer:** B

**Explanation:** Aggregation tables provide fast summaries while keeping detail in DirectQuery.

---

## Question 6 – Time Intelligence

Management requests Year-to-Date Sales compared to the same period last year.

A. TOTALYTD() + SAMEPERIODLASTYEAR()
B. FIRSTDATE()
C. VALUES()
D. REMOVEFILTERS()

**Answer:** A

**Explanation:** TOTALYTD calculates the running total, while SAMEPERIODLASTYEAR shifts the comparison period back one year.

---

## Question 7 – Semantic Models

A Certified Semantic Model already contains all required measures.

A. Download the PBIX and duplicate it.
B. Connect to the Certified Semantic Model.
C. Export to Excel.
D. Re-import the data.

**Answer:** B

**Explanation:** Reusing a Certified Semantic Model promotes consistency and reduces maintenance.

---

## Question 8 – Power Query Errors

After changing a column from Text to Whole Number, only a few rows display Error while the remaining rows load successfully.

A. Step-level error
B. Cell-level error
C. Load error
D. Data source error

**Answer:** B

**Explanation:** Cell-level errors affect only individual values; the query continues to execute.

---

## Question 9 – Model Optimization

Which action is LEAST likely to reduce an imported semantic model's size?

A. Remove unused columns
B. Remove unused rows
C. Add calculated columns
D. Change Decimal to Whole Number when appropriate

**Answer:** C

**Explanation:** Calculated columns are stored in memory and increase model size.

---

## Question 10 – Tenant Settings

Your organization wants users to collaborate internally but prevent anonymous public report links.

A. Disable Export Data
B. Disable Publish to Web
C. Disable Build Permission
D. Disable XMLA Endpoint

**Answer:** B

**Explanation:** The Publish to Web tenant setting controls anonymous internet access while preserving secure internal sharing.

# PL-300 Expert Practice Questions – Set 2

These questions are designed to resemble the reasoning required on the PL-300 exam. Several answers may seem reasonable, but only **one is the best answer** according to Microsoft's recommended practices.

---

# Question 1 – Date Table Optimization

A Microsoft Fabric semantic model contains:

- Auto Date/Time enabled
- 8 fact tables
- 22 Date columns
- Multiple Year-to-Date measures

Users report that refresh time has steadily increased and the semantic model has become much larger.

What should you do FIRST?

A. Convert every Date column to Text.

B. Disable Auto Date/Time and create one marked Date table.

C. Create a Date table for every fact table.

D. Remove all Date relationships.

## Answer

✅ **B**

### Explanation

Auto Date/Time creates a hidden calendar table for every eligible Date column. A single marked Date table reduces model size, improves maintainability, and supports all time intelligence functions.

---

# Question 2 – Minimizing Model Size

A Sales table contains:

- SalesID
- CustomerID
- ProductID
- ProductDescription
- CustomerComments
- SalesAmount

ProductDescription and CustomerComments are never used in reports.

Which action provides the greatest reduction in semantic model size?

A. Hide both columns.

B. Remove both columns during data preparation.

C. Create calculated columns instead.

D. Convert both columns to Whole Number.

## Answer

✅ **B**

### Explanation

Removing unused columns before loading data reduces memory usage. Hiding columns does not reduce model size because they are still loaded into memory.

---

# Question 3 – Query Folding

A Power Query developer performs these transformations:

1. Filter rows
2. Remove columns
3. Merge SQL tables
4. Invoke a custom M function

Performance decreases significantly.

What is the BEST solution?

A. Move the Merge after the custom function.

B. Rewrite the custom function so SQL Server performs the transformation.

C. Convert the semantic model to Import mode.

D. Create calculated columns.

## Answer

✅ **B**

### Explanation

Custom M functions frequently stop query folding. Rewriting the logic so it executes in SQL allows the source system to perform the work and improves refresh performance.

---

# Question 4 – Relationships

A developer creates these relationships:

Customer → Sales

Customer → Returns

Sales → Returns

Users receive ambiguous relationship errors.

What should you do?

A. Make every relationship bidirectional.

B. Remove the unnecessary fact-to-fact relationship.

C. Duplicate the Sales table.

D. Use LOOKUPVALUE() instead.

## Answer

✅ **B**

### Explanation

Fact tables generally should not be directly related. A star schema uses shared dimensions to filter multiple fact tables.

---

# Question 5 – Incremental Refresh

A Fabric semantic model stores seven years of sales history.

Business requirements:

- Refresh only the previous 14 days.
- Keep all historical data available.

Which feature satisfies these requirements?

A. Scheduled Refresh

B. Incremental Refresh

C. Automatic Page Refresh

D. Direct Lake

## Answer

✅ **B**

### Explanation

Incremental Refresh partitions data so that only recent partitions are refreshed while historical partitions remain unchanged.

---

# Question 6 – Dynamic Row-Level Security

A company has 2,000 employees.

Each employee should only see their own sales.

Which solution requires the LEAST maintenance?

A. Create 2,000 security roles.

B. Publish 2,000 reports.

C. Use Dynamic RLS with USERPRINCIPALNAME().

D. Create separate Fabric workspaces.

## Answer

✅ **C**

### Explanation

Dynamic RLS automatically filters data based on the signed-in user's identity, eliminating the need for hundreds or thousands of static roles.

---

# Question 7 – Fabric Workspace

A Fabric workspace contains:

- One Certified Semantic Model
- Twelve reports

A developer modifies an existing measure.

What should report authors do?

A. Republish every report.

B. Download the PBIX files.

C. Refresh the reports connected to the semantic model.

D. Create a new semantic model.

## Answer

✅ **C**

### Explanation

Reports connected to a shared semantic model automatically use updated measures once the semantic model is refreshed.

---

# Question 8 – Time Intelligence

Management requests a measure that always compares the current month with the previous month.

Which DAX function is the BEST choice?

A. PREVIOUSMONTH()

B. SAMEPERIODLASTYEAR()

C. TOTALYTD()

D. FIRSTDATE()

## Answer

✅ **A**

### Explanation

PREVIOUSMONTH() shifts the filter context back exactly one calendar month, matching the business requirement.

---

# Question 9 – Model Optimization

Which change is MOST likely to reduce semantic model size?

A. Hide unused columns.

B. Replace measures with calculated columns.

C. Remove high-cardinality columns that are not required.

D. Convert Whole Numbers to Decimal Numbers.

## Answer

✅ **C**

### Explanation

High-cardinality columns consume significant memory. Removing unnecessary ones can greatly reduce model size.

---

# Question 10 – Tenant Settings

Your organization wants users to:

- Build reports
- Share reports internally
- Prevent anonymous public access

Which tenant setting should be disabled?

A. Build Permission

B. Publish to Web

C. Export Data

D. XMLA Endpoint

## Answer

✅ **B**

### Explanation

Disabling Publish to Web prevents anonymous internet access while still allowing secure sharing within the organization.

---

# PL-300 Exam Tip

When multiple answers seem correct, Microsoft generally prefers the option that follows **Power BI best practices**.

Common examples include:

- ✅ Remove unused columns instead of hiding them.
- ✅ Use one marked Date table instead of Auto Date/Time.
- ✅ Reuse Certified Semantic Models instead of duplicating datasets.
- ✅ Preserve query folding whenever possible.
- ✅ Use Dynamic RLS instead of creating many static roles.
- ✅ Prefer a star schema over fact-to-fact relationships.
- ✅ Use Incremental Refresh for large historical datasets.
- ✅ Remove unnecessary high-cardinality columns to reduce model size.

# PL-300 Expert Practice Questions – Set 3
### Microsoft Exam Style (Mixed Topics)

These questions intentionally combine multiple concepts. More than one answer may seem correct, but only **one is Microsoft's recommended solution**.

---

# Question 1 – Composite Models & Live Connection

A Microsoft Fabric workspace contains a **Certified Semantic Model** used by several reports.

A business analyst creates a new report using a **Live Connection** to the semantic model. They now need to add an Excel spreadsheet containing annual budget targets and create measures that combine Budget and Sales.

What should the analyst do?

A. Import the Excel workbook into the existing Certified Semantic Model.

B. Convert the report to use a local model (DirectQuery for Power BI semantic models/composite model) and import the Excel table.

C. Download the PBIX containing the Certified Semantic Model and modify it.

D. Create report-level measures only.

## Answer

✅ **B**

### Explanation

A Live Connection alone cannot import additional tables. By creating a **composite model (DirectQuery for Power BI semantic models)**, the analyst can extend the model with local tables and new measures while still using the existing semantic model.

---

# Question 2 – Build Permission

A user has **Viewer** access to a Fabric workspace.

They need to create their own report using an existing semantic model but should not be able to edit reports in the workspace.

What additional permission should they receive?

A. Member

B. Contributor

C. Build

D. Admin

## Answer

✅ **C**

### Explanation

**Build** permission allows users to create new reports from a semantic model without granting editing rights to workspace content.

---

# Question 4 – Reference vs Duplicate

A Power Query query named **Sales** has already completed extensive cleaning.

You need another query that should inherit all future changes made to **Sales**, while applying a few additional transformations.

What should you do?

A. Duplicate the query.

B. Reference the query.

C. Copy and paste the query.

D. Export the query to Excel.

## Answer

✅ **B**

### Explanation

A **Reference** creates a dependent query that reflects future changes made to the original query. A **Duplicate** creates an independent copy.

---

# Question 5 – Inactive Relationships

A Sales table contains:

- OrderDate
- ShipDate

The active relationship uses OrderDate.

A report must calculate Sales by ShipDate without changing the active relationship.

Which DAX function should you use?

A. CROSSFILTER()

B. USERELATIONSHIP()

C. REMOVEFILTERS()

D. RELATED()

## Answer

✅ **B**

### Explanation

`USERELATIONSHIP()` temporarily activates an inactive relationship during measure evaluation.

---

# Question 6 – Q&A Visual

A Q&A visual frequently returns incorrect results.

The semantic model uses technical column names such as:

Cust_ID

Prod_Nm

Amt_Sls

What should you do FIRST?

A. Add synonyms and friendly field names.

B. Create calculated columns.

C. Enable Incremental Refresh.

D. Change every field to Text.

## Answer

✅ **A**

### Explanation

Q&A performs best when fields have meaningful names and synonyms that match natural language.

---

# Question 7 – Analyze in Excel

A finance analyst wants to build PivotTables in Excel using a Fabric semantic model.

The analyst has Viewer access to the workspace.

What additional permission is required?

A. Member

B. Contributor

C. Build

D. Admin

## Answer

✅ **C**

### Explanation

Analyze in Excel requires **Build** permission on the semantic model.

---

# Question 8 – Promoted vs Certified

A department creates a semantic model that has been reviewed internally but has not yet been approved by central BI governance.

Which endorsement should be applied?

A. Certified

B. Promoted

C. Archived

D. Shared

## Answer

✅ **B**

### Explanation

**Promoted** indicates that the dataset is useful and recommended by its owners. **Certified** requires formal organizational approval.

---

# Question 9 – Drillthrough

A report page summarizes Sales by Country.

Users want to right-click a country and open another report page showing detailed customer transactions for only that country.

Which feature should be used?

A. Drill Down

B. Drillthrough

C. Cross-filtering

D. Small Multiples

## Answer

✅ **B**

### Explanation

Drillthrough passes the selected filter context to another report page designed for detailed analysis.

---

# Question 10 – Performance Analyzer

Users report that a report page loads slowly.

You need to determine whether the delay is caused by DAX queries, visual rendering, or another factor.

Which tool should you use FIRST?

A. Query Diagnostics

B. Performance Analyzer

C. Data Profiling

D. VertiPaq Analyzer

## Answer

✅ **B**

### Explanation

Performance Analyzer identifies how much time is spent executing DAX queries, rendering visuals, and performing other report operations.

---

# Bonus PL-300 Review

Know these frequently confused pairs:

| Microsoft Likes to Compare | Know the Difference |
|----------------------------|---------------------|
| Reference vs Duplicate | Reference inherits future changes |
| Viewer vs Build | Build allows creating reports |
| Promoted vs Certified | Certified requires governance approval |
| Drill Down vs Drillthrough | Drillthrough opens another page |
| Live Connection vs Composite Model | Composite models allow local tables |
| USERELATIONSHIP vs RELATED | USERELATIONSHIP activates inactive relationships |
| Performance Analyzer vs Query Diagnostics | Performance Analyzer analyzes report performance |

# PL-300 Expert Practice Questions – Set 4
### Mixed Topics (Microsoft Exam Style)

These questions are designed to resemble the reasoning required on the PL-300 exam. Several answers may be technically possible, but only **one is the BEST solution** according to Microsoft's recommended practices.

---

# Question 1 – Merge vs Append

You receive monthly sales files from four regions.

Each file contains the **same columns**:

- OrderID
- OrderDate
- CustomerID
- SalesAmount

You need to create one table containing all sales records.

What should you do?

A. Merge the four queries using a Full Outer join.

B. Append the four queries.

C. Create relationships between the four tables.

D. Use UNION() in DAX.

## ✅ Answer

**B**

### Explanation

Appending combines rows from tables with the same structure.

Merge combines columns from related tables.

**Exam Tip**

> Same columns = **Append**
>
> Related tables = **Merge**

---

# Question 2 – Join Types

Sales contains every sale.

Customers contains only active customers.

Management wants every sale returned, even if a matching customer no longer exists.

Which Merge Join should be used?

A. Inner

B. Left Outer

C. Right Outer

D. Full Outer

## ✅ Answer

**B**

### Explanation

The Sales table is the primary table.

A Left Outer join keeps every row from the first (left) table and matches customer information when available.

---

# Question 3 – USERELATIONSHIP

A Sales table contains:

- OrderDate (Active relationship)
- ShipDate (Inactive relationship)

A report must calculate Total Sales by Ship Date.

What should you do?

A.

```DAX
CALCULATE(
    [Total Sales],
    USERELATIONSHIP(Sales[ShipDate],Date[Date])
)
```

B.

Use RELATED()

C.

Use REMOVEFILTERS()

D.

Create another Date table.

## ✅ Answer

**A**

### Explanation

USERELATIONSHIP temporarily activates an inactive relationship during measure evaluation.

---

# Question 4 – Build Permission

A user has Viewer access to a Fabric workspace.

They need to:

- Create their own report
- Use an existing semantic model
- Not modify workspace content

Which permission should be granted?

A. Member

B. Contributor

C. Build

D. Admin

## ✅ Answer

**C**

### Explanation

Build permission allows report creation without granting editing rights.

---

# Question 5 – Field Parameters

Management wants users to switch a visual between displaying:

- Revenue
- Profit
- Quantity

without creating multiple visuals.

Which feature should be used?

A. Bookmarks

B. Drillthrough

C. Field Parameters

D. Small Multiples

## ✅ Answer

**C**

### Explanation

Field Parameters allow users to dynamically switch displayed measures or dimensions.

---

# Question 6 – Column Quality

A developer wants to quickly determine:

- Valid values
- Empty values
- Error values

for every column in Power Query.

Which profiling feature should they use?

A. Column Distribution

B. Column Quality

C. Column Profile

D. Query Diagnostics

## ✅ Answer

**B**

### Explanation

Column Quality displays the percentage of valid, empty, and error values.

---

# Question 7 – Column Distribution

A developer wants to understand how many distinct values exist in each column and identify the most common values.

Which feature should be used?

A. Column Quality

B. Column Distribution

C. Performance Analyzer

D. Data View

## ✅ Answer

**B**

### Explanation

Column Distribution displays unique values, distinct counts, and frequency distribution.

---

# Question 8 – Sensitivity Labels

A report contains confidential payroll information.

Management wants users to immediately recognize that the report contains sensitive information.

What should be applied?

A. Promote the semantic model.

B. Apply a Sensitivity Label.

C. Certify the report.

D. Create a Perspective.

## ✅ Answer

**B**

### Explanation

Sensitivity Labels classify data (Confidential, Highly Confidential, etc.) and help enforce governance policies.

---

# Question 9 – Relationship Troubleshooting

A report contains these tables:

Sales

↓

Product

↓

Category

A developer also creates a direct relationship between Sales and Category.

Unexpected filtering occurs.

What is the BEST solution?

A. Change every relationship to Bidirectional.

B. Remove the unnecessary relationship.

C. Create another Sales table.

D. Convert Category into a calculated column.

## ✅ Answer

**B**

### Explanation

The additional relationship creates multiple filter paths, leading to ambiguity. A clean star schema should have one clear path.

---

# Question 10 – DATEADD vs PARALLELPERIOD

Management requests a report that compares **the current month with the same month one year earlier**, even when users filter individual days.

Which function is MOST appropriate?

A. DATEADD()

B. PARALLELPERIOD()

C. FIRSTDATE()

D. TOTALMTD()

## ✅ Answer

**A**

### Explanation

DATEADD shifts the current filter context by a specified interval while preserving the selected date range.

PARALLELPERIOD returns an entire shifted period and is generally less appropriate when the current filter context contains partial periods or individual dates.

---

# ⭐ PL-300 Quick Review

| Business Requirement | Best Feature |
|----------------------|--------------|
| Combine rows from identical tables | Append |
| Combine columns from related tables | Merge |
| Keep every row from first table | Left Outer Join |
| Use inactive relationship | USERELATIONSHIP() |
| Create reports from a semantic model | Build Permission |
| Switch measures in one visual | Field Parameters |
| View valid/error/empty values | Column Quality |
| View distinct values and frequency | Column Distribution |
| Classify confidential data | Sensitivity Labels |
| Compare same dates from last year | DATEADD() or SAMEPERIODLASTYEAR() (depending on the business requirement) |