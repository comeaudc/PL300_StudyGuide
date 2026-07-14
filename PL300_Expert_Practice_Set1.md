
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


# PL-300 Expert Practice Questions – Set 5
### Mixed Scenario Questions (Accessibility, Desktop vs Service, Performance, Power Query)

These questions are written to resemble Microsoft's PL-300 exam. Several answers may seem reasonable, but only **one is the BEST solution.**

---

# Question 1 – Accessibility

A report will be distributed throughout your organization.

Several users rely on screen readers to navigate reports.

You need to improve accessibility without changing the report layout.

What should you do?

A. Add Alt Text to each visual.

B. Increase the report page size.

C. Add more bookmarks.

D. Create additional pages.

## ✅ Answer

**A**

### Explanation

Alt Text provides descriptions of visuals for screen readers and is one of Microsoft's primary accessibility recommendations.

---

# Question 2 – Accessibility

A report contains:

- Red bars for losses
- Green bars for profits

Some users have difficulty distinguishing the colors.

What should you do?

A. Increase the font size.

B. Use color alone since the values are correct.

C. Use additional indicators such as labels or patterns instead of relying only on color.

D. Create another report.

## ✅ Answer

**C**

### Explanation

Power BI accessibility guidance recommends **not relying solely on color** to communicate information.

---

# Question 3 – Desktop vs Service

A report author creates a report in Power BI Desktop.

They publish both the report and semantic model to a Microsoft Fabric workspace.

The report should refresh automatically every morning.

Where should the refresh schedule be configured?

A. Power BI Desktop

B. Microsoft Fabric (Power BI Service)

C. Power Query Editor

D. DAX Studio

## ✅ Answer

**B**

### Explanation

Scheduled Refresh is configured after publishing in the Power BI Service (Fabric), not in Desktop.

---

# Question 4 – Desktop vs Service

A report refreshes successfully in Power BI Desktop.

After publishing, scheduled refresh fails because the data source is an on-premises SQL Server.

What is the MOST likely cause?

A. The semantic model is too large.

B. An On-premises Data Gateway has not been configured.

C. The report contains bookmarks.

D. Query folding is disabled.

## ✅ Answer

**B**

### Explanation

The Power BI Service cannot directly access on-premises data sources without an On-premises Data Gateway.

---

# Question 5 – Power Query Join

You have two tables:

Orders

Customers

You need to keep **every order**, even if no matching customer record exists.

Which merge option should you choose?

A. Only matching rows

B. All rows from Orders and matching rows from Customers

C. Only rows that exist in both tables and nowhere else

D. Only rows from Customers

## ✅ Answer

**B**

### Explanation

This describes a **Left Outer** merge without using join terminology. Every record from the first table is preserved.

---

# Question 6 – Power Query Merge

A Product table contains discontinued products.

A Sales table contains every product ever sold.

You need a list of products that **have never been sold**.

Which merge result should you choose?

A. Keep only matching rows.

B. Keep all rows from Sales.

C. Keep only rows from Product that have no matching Sales record.

D. Append the tables.

## ✅ Answer

**C**

### Explanation

This is the behavior of a **Left Anti** merge. It returns rows from the first table that have **no corresponding match** in the second table.

---

# Question 7 – Data Profiling

A developer wants to determine:

- Percentage of valid values
- Percentage of empty values
- Percentage of error values

Which Power Query feature should be used?

A. Column Distribution

B. Column Profile

C. Column Quality

D. Performance Analyzer

## ✅ Answer

**C**

### Explanation

Column Quality summarizes each column by showing the percentages of valid, empty, and error values.

---

# Question 8 – Data Profiling

A developer wants to understand:

- Number of distinct values
- Number of unique values
- Most frequently occurring values

Which Power Query feature should be used?

A. Column Quality

B. Column Distribution

C. Column Profile

D. Query Diagnostics

## ✅ Answer

**B**

### Explanation

Column Distribution displays distinct values, unique values, and value frequency.

---

# Question 9 – Data Profiling

A developer needs detailed statistics for a single numeric column, including:

- Minimum
- Maximum
- Average
- Standard deviation
- Value distribution

Which feature should be used?

A. Column Profile

B. Column Quality

C. Column Distribution

D. Data View

## ✅ Answer

**A**

### Explanation

Column Profile provides comprehensive statistics and detailed analysis for an individual column.

---

# Question 10 – Performance Analyzer

Users report that a report page loads slowly.

You need to determine whether the delay is caused by:

- DAX queries
- Visual rendering
- Other processing

Which tool should you use FIRST?

A. Query Diagnostics

B. Performance Analyzer

C. Power Query Editor

D. Model View

## ✅ Answer

**B**

### Explanation

Performance Analyzer breaks report execution into DAX query time, visual display time, and other processing, making it the first tool to identify report performance bottlenecks.

---

# ⭐ PL-300 Quick Review

| Requirement | Best Feature |
|--------------|-------------|
| Describe visuals for screen readers | Alt Text |
| Don't rely only on color | Labels, icons, or patterns |
| Configure scheduled refresh | Power BI Service (Fabric) |
| Refresh on-premises SQL | On-premises Data Gateway |
| Keep all rows from first table | "All rows from first table and matching rows from second" |
| Find records without matches | "Only rows from first table with no matches" |
| Valid / Empty / Error percentages | Column Quality |
| Distinct values & frequency | Column Distribution |
| Detailed statistics for one column | Column Profile |
| Analyze report rendering performance | Performance Analyzer |

## 🚨 Exam Tip

Microsoft often describes merge operations **without naming the join type**. Focus on the behavior:

- **Keep all rows from the first table** → Left Outer
- **Keep only matching rows** → Inner
- **Keep only rows from the first table with no match** → Left Anti
- **Keep only rows from the second table with no match** → Right Anti

Understanding the result is more important than memorizing the join names.


# PL-300 Expert Practice Questions – Set 5
### Power BI Service vs Desktop | Performance Analyzer | Publishing | Refresh | Sharing

These questions are intentionally written to resemble Microsoft's PL-300 exam. Several answers may be technically correct, but only one is the **BEST** solution.

---

# Question 1 – Desktop vs Service

A report author creates a report in **Power BI Desktop**.

Business users request a dashboard that pins visuals from multiple reports and allows alerting on KPI tiles.

Where must this functionality be created?

A. Power BI Desktop

B. Power Query Editor

C. Power BI Service

D. DAX Studio

## ✅ Answer

**C**

### Explanation

Dashboards only exist in the **Power BI Service**.

Desktop creates reports.

Service provides:

- Dashboards
- Apps
- Sharing
- Subscriptions
- Data Alerts

---

# Question 2 – Performance Analyzer

A report page requires 18 seconds to load.

Performance Analyzer returns the following:

| Component | Time |
|------------|------|
| DAX Query | 14 sec |
| Visual Display | 1 sec |
| Other | 3 sec |

What should you investigate FIRST?

A. The visual formatting

B. The DAX measures

C. Report theme

D. Bookmarks

## ✅ Answer

**B**

### Explanation

The majority of execution time occurs in the DAX query.

Optimizing measures, relationships, filter context, or model design will have the greatest impact.

---

# Question 3 – Performance Analyzer

Performance Analyzer shows:

| Component | Time |
|------------|------|
| DAX Query | 0.4 sec |
| Visual Display | 8 sec |
| Other | 0.3 sec |

What is the MOST likely cause?

A. Inefficient DAX

B. Too many visual elements being rendered

C. Missing relationships

D. Query folding has stopped

## ✅ Answer

**B**

### Explanation

The data is retrieved quickly.

Rendering the visual itself is taking most of the time.

Large matrices, maps, custom visuals, and excessive conditional formatting often increase rendering time.

---

# Question 4 – Publishing

A developer publishes an updated PBIX file to a Fabric workspace.

The report already exists in the workspace.

What happens?

A. A second report is created automatically.

B. The existing report and semantic model are replaced.

C. Only the report is updated.

D. Only the semantic model is updated.

## ✅ Answer

**B**

### Explanation

Publishing the same PBIX replaces both the report and semantic model unless different publishing techniques are used.

---

# Question 5 – Scheduled Refresh

A semantic model refreshes successfully in Desktop.

After publishing to the Power BI Service, scheduled refresh fails.

The source is an on-premises SQL Server.

What is the MOST likely cause?

A. Query folding stopped.

B. A gateway has not been configured.

C. Auto Date/Time is disabled.

D. Relationships are inactive.

## ✅ Answer

**B**

### Explanation

The Power BI Service cannot directly access on-premises data sources.

An On-premises Data Gateway is required.

---

# Question 6 – Service Permissions

A manager should:

- View reports
- Create new reports using an existing semantic model
- Not edit workspace content

Which combination is BEST?

A. Viewer + Build permission

B. Member

C. Contributor

D. Admin

## ✅ Answer

**A**

### Explanation

Viewer allows viewing workspace content.

Build permission allows creating reports from semantic models.

Neither grants editing rights.

---

# Question 7 – Dashboards

A dashboard contains tiles pinned from four different reports.

One report is updated and republished.

What happens?

A. The dashboard tile automatically reflects the updated report.

B. The dashboard must be recreated.

C. The dashboard becomes disconnected.

D. Every tile must be repinned.

## ✅ Answer

**A**

### Explanation

Pinned dashboard tiles continue referencing the report.

Republishing the report updates the dashboard automatically.

---

# Question 8 – Performance Optimization

A report page contains:

- 24 visuals
- 9 slicers
- 5 cards
- 3 matrices

Users complain that opening the page is slow.

Which change is MOST likely to improve report performance?

A. Increase font sizes.

B. Reduce the number of visuals displayed simultaneously.

C. Change every visual to a table.

D. Add more slicers.

## ✅ Answer

**B**

### Explanation

Each visual sends queries and requires rendering.

Reducing unnecessary visuals often produces immediate performance improvements.

---

# Question 9 – Analyze Performance

Performance Analyzer reports:

| Component | Time |
|------------|------|
| DAX Query | 1 sec |
| Visual Display | 0.8 sec |
| Other | 12 sec |

What should you investigate FIRST?

A. DAX calculations

B. Model relationships

C. Visual rendering

D. Visual interactions, page navigation, or external processes

## ✅ Answer

**D**

### Explanation

"Other" includes activities such as waiting for visuals, page processing, and miscellaneous client-side operations.

Since "Other" dominates the execution time, DAX optimization is unlikely to solve the issue.

---

# Question 10 – Service vs Desktop

Which feature is available **only** in the Power BI Service?

A. Power Query Editor

B. Performance Analyzer

C. Data Alerts

D. Relationship View

## ✅ Answer

**C**

### Explanation

Data Alerts can only be configured in the Power BI Service.

Desktop includes:

- Modeling
- Relationships
- Performance Analyzer
- Power Query

Service includes:

- Dashboards
- Apps
- Data Alerts
- Sharing
- Subscriptions
- Usage Metrics

---

# ⭐ PL-300 Desktop vs Service Review

| Feature | Desktop | Service |
|----------|:-------:|:-------:|
| Build Reports | ✅ | Limited editing |
| Power Query Editor | ✅ | ❌ |
| Model View | ✅ | ❌ |
| Relationships | ✅ | ❌ |
| Performance Analyzer | ✅ | ❌ |
| Publish Reports | ✅ | ✅ |
| Dashboards | ❌ | ✅ |
| Apps | ❌ | ✅ |
| Data Alerts | ❌ | ✅ |
| Subscriptions | ❌ | ✅ |
| Scheduled Refresh | ❌ | ✅ |
| Usage Metrics | ❌ | ✅ |
| Share Reports | ❌ | ✅ |
| Manage Workspace Roles | ❌ | ✅ |

---

# ⭐ PL-300 Performance Analyzer Cheat Sheet

When reading Performance Analyzer results, focus on the **largest value**:

| Largest Time | Investigate |
|---------------|-------------|
| **DAX Query** | Measures, filter context, relationships, model design |
| **Visual Display** | Complex visuals, matrices, maps, custom visuals, excessive formatting |
| **Other** | Page interactions, client processing, visual dependencies, miscellaneous operations |

**Exam Tip:** On the PL-300, Microsoft often gives you Performance Analyzer timings. The correct answer is usually the component with the **highest execution time**, since that's where optimization will have the greatest impact.

# PL-300 Expert Practice Questions – Set 6
## Microsoft PL-300 Style (Mixed Topics)
---

# Question 1 – Performance Analyzer

A report page contains six visuals.

Performance Analyzer returns the following results:

| Visual | DAX Query | Visual Display |
|---------|----------:|---------------:|
| Sales by Product | 0.4 sec | 0.3 sec |
| Sales by Customer | 5.8 sec | 0.4 sec |
| Monthly Trend | 0.5 sec | 0.2 sec |
| KPI Cards | 0.2 sec | 0.1 sec |

You need to improve report performance.

What should you investigate first?

A. The Product visual formatting

B. The DAX measures and model used by **Sales by Customer**

C. The report theme

D. The page background image

## ✅ Answer

**B**

### Explanation

Performance Analyzer shows that almost all of the delay comes from the DAX query for one visual. Optimizing that measure or its model will have the greatest impact.

---

# Question 2 – Matrix vs Table

Management wants a report showing:

- Product Categories
- Products beneath each category
- Sales by Year
- Expand/Collapse buttons
- Row subtotals

Which visual should you use?

A. Table

B. Matrix

C. Multi-row Card

D. Clustered Column Chart

## ✅ Answer

**B**

### Explanation

A Matrix supports hierarchical rows, expandable groups, subtotals, and values across columns. A Table cannot create expandable hierarchies.

---

# Question 3 – Matrix Requirements

A finance report should display:

```
Region
   Product Category
      Product
```

Users should be able to drill into lower levels and collapse the hierarchy.

Which visual best satisfies the requirement?

A. Table

B. Matrix

C. Treemap

D. Decomposition Tree

## ✅ Answer

**B**

### Explanation

The Matrix visual is specifically designed for hierarchical row structures with expand/collapse functionality.

---

# Question 4 – Performance Analyzer

Performance Analyzer reports:

| Component | Time |
|-----------|------|
| DAX Query | 0.6 sec |
| Visual Display | 7.9 sec |
| Other | 0.4 sec |

Which action is MOST likely to improve performance?

A. Rewrite DAX measures

B. Reduce the complexity or number of visuals

C. Create additional relationships

D. Change storage mode

## ✅ Answer

**B**

### Explanation

The DAX query is already fast. Most of the delay occurs while rendering the visual.

---

# Question 5 – Visual Interactions

A report contains:

- A bar chart
- A map
- A KPI card

Selecting a bar in the chart filters the map, but management wants the KPI card to remain unchanged.

What should you do?

A. Disable cross-highlighting.

B. Edit Visual Interactions.

C. Remove the relationship.

D. Duplicate the KPI card.

## ✅ Answer

**B**

### Explanation

Edit Interactions allows you to control which visuals filter, highlight, or ignore each other.

---

# Question 6 – Field Parameters

A report currently contains three identical charts:

- Revenue
- Profit
- Margin

Management wants only one chart while allowing users to choose which metric to display.

What is the BEST solution?

A. Bookmarks

B. Drillthrough

C. Field Parameters

D. Conditional Formatting

## ✅ Answer

**C**

### Explanation

Field Parameters allow users to dynamically switch the displayed measure without creating multiple visuals.

---

# Question 7 – Small Multiples

Management wants to compare monthly sales trends for every sales region using identical line charts displayed in a grid.

Which visual feature should you use?

A. Drillthrough

B. Matrix

C. Small Multiples

D. Bookmarks

## ✅ Answer

**C**

### Explanation

Small Multiples display the same visual repeatedly for each category, making comparisons much easier.

---

# Question 8 – Tooltip Pages

Users want additional product details to appear only when hovering over a visual.

Which feature should you implement?

A. Drillthrough

B. Tooltip Page

C. Bookmark

D. Q&A

## ✅ Answer

**B**

### Explanation

Report Tooltip pages display detailed information when users hover over a data point without navigating away from the report.

---

# Question 9 – Conditional Formatting

A manager wants Sales values to appear:

- Green when above target
- Red when below target

Which feature should be used?

A. Themes

B. Conditional Formatting

C. Bookmarks

D. Slicers

## ✅ Answer

**B**

### Explanation

Conditional Formatting dynamically changes colors or icons based on business rules.

---

# Question 10 – Choosing the Correct Visual

Management wants a report that answers:

> "Which factors most strongly influence whether customers purchase premium products?"

Which visual should you recommend?

A. Matrix

B. Scatter Chart

C. Key Influencers

D. Waterfall Chart

## ✅ Answer

**C**

### Explanation

The Key Influencers visual uses statistical analysis to identify the factors that most influence a selected outcome.

---

# ⭐ PL-300 Visual Selection Cheat Sheet

| Business Requirement | Best Visual |
|----------------------|-------------|
| Hierarchical rows with expand/collapse | **Matrix** |
| Flat list of records | **Table** |
| Compare many identical charts | **Small Multiples** |
| Explain what drives an outcome | **Key Influencers** |
| Break down contributors interactively | **Decomposition Tree** |
| Show extra information on hover | **Tooltip Page** |
| Switch between measures or dimensions | **Field Parameters** |
| Apply colors/icons based on values | **Conditional Formatting** |
| Control how visuals affect each other | **Edit Interactions** |

---

### 💡 PL-300 Exam Tip

Microsoft often describes a business requirement rather than naming the feature directly. Learn to recognize the keywords:

- **Expand / Collapse** → Matrix
- **Hover for details** → Tooltip Page
- **Choose Revenue or Profit** → Field Parameters
- **Why did this happen?** → Key Influencers
- **Break down by category interactively** → Decomposition Tree
- **Show many identical charts by category** → Small Multiples
- **One visual should not filter another** → Edit Interactions