
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

# PL-300 Expert Practice Questions – Set 7
### Microsoft Exam Style (Mixed Topics)

These questions are designed to resemble the reasoning required on the PL-300 exam. Several answers may appear correct, but only **one is the BEST solution** according to Microsoft's recommended practices.

---

# Question 1 – Pivot vs Unpivot

A sales spreadsheet contains one row per product.

| Product | Jan | Feb | Mar | Apr |
|----------|----:|----:|----:|----:|
| Bike | 120 | 145 | 131 | 150 |
| Helmet | 55 | 61 | 58 | 66 |

You need to create a line chart showing sales by month.

What should you do in Power Query?

A. Pivot the Month columns.

B. Unpivot the Month columns.

C. Merge the table with itself.

D. Group By Product.

## ✅ Answer

**B**

### Explanation

Power BI visuals work best when dates are stored as values in a single column instead of separate columns. Unpivoting creates a structure like:

| Product | Month | Sales |

which is ideal for charts and DAX.

---

# Question 2 – Append vs Merge

You have:

**Orders**

| OrderID | CustomerID |

**Customers**

| CustomerID | CustomerName |

You need to display the customer name beside every order.

Which transformation should you use?

A. Append Queries

B. Merge Queries

C. Pivot

D. Unpivot

## ✅ Answer

**B**

### Explanation

Merge combines related tables by matching keys. Append combines rows from tables with the same structure.

---

# Question 3 – Many-to-Many Relationships

A bridge table has already been created between Customers and Promotions.

A developer suggests creating a direct relationship between Customers and Promotions as well.

What is the BEST recommendation?

A. Create the additional relationship.

B. Replace the bridge table with calculated columns.

C. Keep only the bridge-table relationship.

D. Make both relationships bidirectional.

## ✅ Answer

**C**

### Explanation

A bridge table is the recommended approach for resolving many-to-many relationships. Adding another direct relationship can create ambiguity and unexpected filter behavior.

---

# Question 4 – CALCULATE()

A report contains a Region slicer.

Management wants a measure that always returns total company sales regardless of the selected Region.

Which measure should be used?

A.

```DAX
CALCULATE([Total Sales], REMOVEFILTERS(Region))
```

B.

```DAX
SUM(Sales[SalesAmount])
```

C.

```DAX
AVERAGE(Sales[SalesAmount])
```

D.

```DAX
COUNTROWS(Sales)
```

## ✅ Answer

**A**

### Explanation

`CALCULATE()` modifies filter context. `REMOVEFILTERS()` ignores the Region filter while respecting all other report filters.

---

# Question 5 – Data Profiling

A developer wants to inspect every value within a selected column, including:

- Value distribution
- Statistics
- Distinct count

Which Power Query feature should they use?

A. Column Quality

B. Column Distribution

C. Column Profile

D. Query Diagnostics

## ✅ Answer

**C**

### Explanation

Column Profile provides the most detailed statistics for a selected column, including min, max, average, distinct values, and value distribution.

---

# Question 6 – Sync Slicers

A report contains five pages.

Management wants one Date slicer that automatically applies the same selection across every page.

What should you do?

A. Copy the slicer onto every page.

B. Use Sync Slicers.

C. Create bookmarks.

D. Create Field Parameters.

## ✅ Answer

**B**

### Explanation

Sync Slicers keeps slicer selections consistent across multiple report pages.

---

# Question 7 – Publish vs Share

A report has been published to a Fabric workspace.

Business users cannot find the report.

What should you do FIRST?

A. Export the report to Excel.

B. Share the report or distribute it through a Power BI App.

C. Republish the PBIX.

D. Create a dashboard.

## ✅ Answer

**B**

### Explanation

Publishing a report places it in a workspace. Users still need permission through direct sharing or a published App before they can access it.

---

# Question 8 – Star Schema

A Sales table contains:

- Customer Name
- Customer City
- Customer State
- Customer Country

These values repeat millions of times.

What is the BEST redesign?

A. Leave the table unchanged.

B. Create a Customer dimension table and relate it to Sales.

C. Duplicate the Sales table.

D. Hide the customer columns.

## ✅ Answer

**B**

### Explanation

Moving descriptive attributes into dimension tables reduces redundancy, improves compression, and follows star schema best practices.

---

# Question 9 – Choosing the Correct Visual

Management asks:

> "Show how Total Sales changed after discounts were applied, shipping costs were added, and taxes were included."

Which visual is MOST appropriate?

A. Scatter Chart

B. Waterfall Chart

C. Matrix

D. Pie Chart

## ✅ Answer

**B**

### Explanation

A Waterfall chart highlights how sequential increases and decreases contribute to a final total.

---

# Question 10 – DAX Measures vs Calculated Columns

A report needs to calculate Total Profit using the current filter context selected by users.

Which approach is BEST?

A. Create a calculated column.

B. Create a measure.

C. Duplicate the Profit column.

D. Create another table.

## ✅ Answer

**B**

### Explanation

Measures are calculated at query time and automatically respond to slicers and filters. Calculated columns are computed during refresh and do not dynamically respond to report filter context in the same way.

---

# ⭐ PL-300 Quick Review

| Requirement | Best Choice |
|--------------|-------------|
| Convert month columns into rows | **Unpivot** |
| Combine related tables | **Merge** |
| Stack tables with the same columns | **Append** |
| Ignore a slicer in a calculation | **CALCULATE() + REMOVEFILTERS()** |
| Detailed column statistics | **Column Profile** |
| Show valid/error/empty percentages | **Column Quality** |
| Show value frequency | **Column Distribution** |
| Same slicer on multiple pages | **Sync Slicers** |
| Repeating descriptive data | **Dimension Table (Star Schema)** |
| Show sequential increases/decreases | **Waterfall Chart** |
| Dynamic calculations | **Measure** |

# PL-300 Expert Practice Questions – Set 8
## Microsoft Exam Style (Advanced Mixed Topics)

These questions are designed to closely match the style of the PL-300 exam. Many answers may seem reasonable, but choose the **BEST** answer based on Microsoft's recommended practices.

---

# Question 1 – Active vs Inactive Relationships

A semantic model contains the following tables:

**Sales**

- OrderDate
- ShipDate
- SalesAmount

**Date**

An active relationship exists between **Sales[OrderDate]** and **Date[Date]**.

A report author creates a visual showing Sales by Ship Date, but the visual still displays sales by Order Date.

You need to correct the calculation without changing the active relationship.

What should you do?

A. Create a second Date table.

B. Use USERELATIONSHIP() in the measure.

C. Change the relationship to bidirectional.

D. Replace the Date table.

## ✅ Answer

**B**

### Explanation

USERELATIONSHIP() temporarily activates an inactive relationship during measure evaluation without affecting the model.

---

# Question 2 – Visual Choice

Management wants users to answer questions such as:

- "Which region contributed most to the increase in sales?"
- "Continue drilling into Product Category, Product, then Customer."

Which visual best satisfies this requirement?

A. Matrix

B. Decomposition Tree

C. Waterfall Chart

D. Treemap

## ✅ Answer

**B**

### Explanation

The Decomposition Tree allows users to interactively drill into multiple dimensions and analyze contributors to a metric.

---

# Question 3 – Cross Filtering

Selecting a state on a map highlights bars in a chart.

Management wants the chart to filter instead of highlight.

What should you do?

A. Edit Interactions.

B. Disable relationships.

C. Create bookmarks.

D. Use Drillthrough.

## ✅ Answer

**A**

### Explanation

Edit Interactions lets you change whether visuals filter, highlight, or ignore one another.

---

# Question 4 – Reference vs Duplicate

A Power Query query named **Sales_Clean** is updated every week.

Another query should always inherit the latest cleaning steps before additional transformations are applied.

Which option should you use?

A. Duplicate

B. Reference

C. Merge

D. Append

## ✅ Answer

**B**

### Explanation

A Reference inherits future changes made to the original query, making maintenance easier.

---

# Question 5 – Visual Performance

A Matrix visual contains:

- 7 hierarchy levels
- Conditional formatting
- Data bars
- Icons
- Thousands of rows

Performance Analyzer shows:

- DAX Query = 0.8 sec
- Visual Display = 10.6 sec

Which recommendation is BEST?

A. Rewrite every measure.

B. Simplify the Matrix visual.

C. Create more calculated columns.

D. Change every relationship to bidirectional.

## ✅ Answer

**B**

### Explanation

The bottleneck is rendering the Matrix, not executing DAX.

---

# Question 6 – Power Query

A CSV file contains these columns:

```
Customer

Phone1

Phone2

Phone3
```

The business wants:

```
Customer

Phone Type

Phone Number
```

Which transformation should you use?

A. Merge

B. Pivot

C. Unpivot

D. Split Column

## ✅ Answer

**C**

### Explanation

Unpivot converts multiple columns into attribute/value pairs, creating a normalized structure.

---

# Question 7 – Report Design

A report contains twelve slicers.

Users complain they spend too much time selecting filters every morning.

Management wants yesterday's selections to automatically appear the next day.

Which feature should users use?

A. Bookmarks

B. Personal Bookmarks

C. Field Parameters

D. Drillthrough

## ✅ Answer

**B**

### Explanation

Personal Bookmarks allow individual users to save and restore their own report state without affecting other users.

---

# Question 8 – DAX

Management asks for a measure that returns the selected product name.

If multiple products are selected, the measure should return "Multiple Products."

Which function is most appropriate?

A. VALUES()

B. SELECTEDVALUE()

C. DISTINCT()

D. RELATED()

## ✅ Answer

**B**

### Explanation

SELECTEDVALUE() returns a single value when one exists and an alternate result when multiple values are selected.

---

# Question 9 – Model Optimization

A Product dimension contains:

- ProductID
- ProductName
- ProductDescription
- WarrantyTerms
- MarketingNotes

Only ProductName is used in reports.

Which action follows Microsoft's recommended practice?

A. Hide the unused columns.

B. Remove unused columns in Power Query.

C. Move the columns into another table within the semantic model.

D. Convert the columns to Whole Number.

## ✅ Answer

**B**

### Explanation

Removing unused columns before loading them reduces memory usage and improves refresh performance.

---

# Question 10 – Power BI Service

A report has been published to a Fabric workspace.

Management wants employees to access a curated collection of reports and dashboards without giving them access to the workspace itself.

What should you create?

A. A Dashboard

B. A Power BI App

C. A Perspective

D. A Deployment Pipeline

## ✅ Answer

**B**

### Explanation

Power BI Apps provide users with a curated, read-only experience while allowing workspace owners to continue developing content independently.

---

# ⭐ PL-300 Review Notes

| Requirement | Best Feature |
|-------------|--------------|
| Use inactive relationship | USERELATIONSHIP() |
| Interactive root-cause analysis | Decomposition Tree |
| Change filter/highlight behavior | Edit Interactions |
| Inherit another query's transformations | Reference |
| Convert repeated columns into rows | Unpivot |
| Save personal report state | Personal Bookmarks |
| Return one selected value | SELECTEDVALUE() |
| Remove unused columns | Power Query |
| Curated report distribution | Power BI App |
| Optimize a slow Matrix | Reduce visual complexity before rewriting DAX if rendering is the bottleneck |

---

## 🚨 PL-300 Exam Traps

### Matrix vs Table

- **Matrix** = Hierarchies, subtotals, expand/collapse.
- **Table** = Flat list of records.

---

### Report vs Dashboard

- **Reports** → Multiple pages, interactive visuals.
- **Dashboards** → One page, Service only, can combine visuals from multiple reports.

---

### App vs Workspace

- **Workspace** → Where developers build and collaborate.
- **App** → How business users consume finished content.

---

### Reference vs Duplicate

- **Reference** → Inherits future changes.
- **Duplicate** → Independent copy.

---

### Highlight vs Filter

If a question asks:
> "Change how visuals interact"

The answer is almost always:

✅ **Edit Interactions**

# PL-300 Expert Practice Questions – Set 9
## Advanced Mixed Topics (Lesser-Tested Objectives)

These questions focus on PL-300 topics that are often overlooked during studying but still appear on the exam. Several answers may seem reasonable, but only **one is the BEST answer**.

---

# Question 1 – Assume Referential Integrity

A semantic model uses DirectQuery to connect to SQL Server.

The Sales table references the Product table through ProductID.

The database administrator confirms that every ProductID in Sales always exists in Product.

You want to improve query performance.

What should you do?

A. Change the relationship to Many-to-Many.

B. Enable **Assume Referential Integrity** on the relationship.

C. Change the relationship to Bidirectional.

D. Import the Product table.

## ✅ Answer

**B**

### Explanation

For DirectQuery models, enabling **Assume Referential Integrity** allows Power BI to generate INNER JOINs instead of OUTER JOINs, which can improve query performance when referential integrity is guaranteed.

---

# Question 2 – Data Profiling

While cleaning a CSV file, you want to determine whether the data contains unexpected values such as "N/A", "Unknown", or misspellings.

Which Power Query feature should you use FIRST?

A. Column Quality

B. Column Distribution

C. Column Profile

D. Query Diagnostics

## ✅ Answer

**C**

### Explanation

Column Distribution quickly shows the frequency of values, making unexpected values easy to identify.

Column Profile provides more detailed statistics but is generally used after identifying potential issues.

---

# Question 3 – Accessibility

A report will be used by employees who rely on screen readers.

Which action best improves report accessibility?

A. Use only custom visuals.

B. Add Alt Text to report visuals.

C. Increase every font size to 24 pt.

D. Disable cross-filtering.

## ✅ Answer

**B**

### Explanation

Alternative text (Alt Text) allows screen readers to describe visuals, improving accessibility.

---

# Question 4 – Q&A Visual

A Q&A visual rarely returns the expected results.

The semantic model uses friendly column names, but users ask questions using company-specific terminology.

What should you do?

A. Add synonyms to the semantic model.

B. Create calculated columns.

C. Enable Auto Date/Time.

D. Change every column to Text.

## ✅ Answer

**A**

### Explanation

Adding synonyms helps Q&A recognize business terminology and improves natural language queries.

---

# Question 5 – Optimize Ribbon

A report page loads slowly.

You want to identify visuals that negatively affect performance without changing the report.

Which tool should you use FIRST?

A. Optimize ribbon

B. Performance Analyzer

C. Query Diagnostics

D. DAX Studio

## ✅ Answer

**B**

### Explanation

Performance Analyzer identifies how much time each visual spends running DAX queries, rendering, and other operations. It is the first tool to diagnose report performance.

---

# Question 6 – Conditional Formatting

A matrix displays yearly sales.

Management wants an icon to appear next to values that exceed the annual sales target.

Which feature should you use?

A. Bookmarks

B. Conditional Formatting

C. Field Parameters

D. Report Tooltips

## ✅ Answer

**B**

### Explanation

Conditional Formatting supports icons, colors, and data bars based on business rules.

---

# Question 7 – Import vs DirectQuery

A company refreshes its data warehouse once each night.

Report users expect the fastest possible report performance during the day.

Which storage mode should you recommend?

A. DirectQuery

B. Import

C. Live Connection

D. Dual for every table

## ✅ Answer

**B**

### Explanation

If data changes only nightly, Import mode provides the best query performance because all data is stored in memory.

---

# Question 8 – Drillthrough

A report summarizes sales by salesperson.

Users frequently ask:

> "Show me all invoices for this salesperson."

What is the BEST solution?

A. Drillthrough

B. Bookmark

C. Tooltip Page

D. Small Multiples

## ✅ Answer

**A**

### Explanation

Drillthrough allows users to navigate to a detailed page while preserving the selected filter context.

---

# Question 9 – Power Query Parameters

A report must connect to either the Development or Production SQL Server.

Developers want to switch environments without editing every query.

What should you create?

A. A calculated column

B. A Power Query Parameter

C. A Field Parameter

D. A hierarchy

## ✅ Answer

**B**

### Explanation

Power Query Parameters allow connection information and other values to be changed centrally without rewriting queries.

---

# Question 10 – Data Reduction

A scatter chart displays 2 million data points.

Users report that the visual is difficult to interpret and performs poorly.

What should you do FIRST?

A. Replace the scatter chart with a table.

B. Aggregate the data before displaying it.

C. Increase the report canvas size.

D. Add more data labels.

## ✅ Answer

**B**

### Explanation

Displaying millions of individual points is both inefficient and difficult to analyze. Aggregating the data improves readability and performance.

---

# ⭐ PL-300 Review

| Requirement | Best Feature |
|-------------|--------------|
| Improve DirectQuery joins | Assume Referential Integrity |
| Find unexpected values | Column Distribution |
| Improve accessibility | Alt Text |
| Improve Q&A | Synonyms |
| Diagnose report performance | Performance Analyzer |
| Show icons/colors by value | Conditional Formatting |
| Fastest report performance with nightly refresh | Import Mode |
| Navigate to filtered detail page | Drillthrough |
| Switch between Dev and Prod | Power Query Parameters |
| Improve charts with excessive detail | Aggregate data |

---

## 🚨 PL-300 Exam Tips

### Column Profiling Tools

| Tool | Primary Purpose |
|------|-----------------|
| **Column Quality** | Valid, Error, Empty percentages |
| **Column Distribution** | Distinct values and frequency |
| **Column Profile** | Detailed statistics for one column |

---

### Import vs DirectQuery

Microsoft generally favors:

- **Import** when the data is relatively static and performance is the priority.
- **DirectQuery** when near-real-time access to source data is required or the dataset is too large to import.

---

### Field Parameters vs Power Query Parameters

This is a common point of confusion:

- **Field Parameters** → Let report consumers switch measures or dimensions in visuals.
- **Power Query Parameters** → Let report authors control connections, filters, or other query values during data preparation.

Remember: **Field Parameters affect the report experience; Power Query Parameters affect data retrieval and transformation.**

# PL-300 Expert Practice Questions – Set 11
## Mixed Topics (Less Repeated Exam Objectives)

---

# Question 1 – Visual Interactions

A report page contains:

- A bar chart
- A map
- A table
- A KPI card

Selecting a state in the map should:

- Filter the table
- Filter the bar chart
- Leave the KPI card unchanged

What should you do?

A. Disable the relationship.

B. Edit Visual Interactions.

C. Create a bookmark.

D. Duplicate the KPI card.

## ✅ Answer

**B**

### Explanation

Edit Interactions allows each visual to either filter, highlight, or ignore another visual independently.

---

# Question 2 – Drillthrough vs Tooltip

Users frequently ask:

> "Can I hover over a customer and immediately see last year's sales without leaving the page?"

Which feature should you use?

A. Drillthrough

B. Tooltip Page

C. Bookmarks

D. Q&A

## ✅ Answer

**B**

### Explanation

Tooltip Pages display additional information without navigating away from the report.

---

# Question 3 – Report Pages

Management wants executives to see only three summary pages, while analysts should have access to all fifteen report pages.

What is the BEST solution?

A. Duplicate the report.

B. Hide the detailed pages before publishing the executive report.

C. Create a dashboard.

D. Create another workspace.

## ✅ Answer

**B**

### Explanation

Hidden pages remain available to report authors but are not shown during normal report navigation.

---

# Question 4 – Data Categories

A report contains a column named PostalCode.

Power BI attempts to plot the values incorrectly on a map.

What should you configure?

A. Default Summarization

B. Data Category

C. Sort by Column

D. Format String

## ✅ Answer

**B**

### Explanation

Setting the correct Data Category (Postal Code) helps Power BI interpret geographic fields correctly.

---

# Question 5 – Sort by Column

Month names appear alphabetically:

April

August

December

...

How should you correct this?

A. Create a hierarchy.

B. Sort MonthName by MonthNumber.

C. Rename the months.

D. Use a Matrix visual.

## ✅ Answer

**B**

### Explanation

Sort by Column lets you display month names while sorting them using a numeric month column.

---

# Question 6 – Default Summarization

A ZIP Code column is automatically summed in visuals.

What should you do?

A. Convert the column to Decimal.

B. Change Default Summarization to **Don't Summarize**.

C. Create a hierarchy.

D. Create a measure.

## ✅ Answer

**B**

### Explanation

Identifiers such as ZIP codes should not be aggregated.

---

# Question 7 – Hierarchies

A report contains separate fields for:

Country

State

City

Users frequently drill through these levels.

Which modeling feature simplifies report creation?

A. Measures

B. Hierarchy

C. Calculation Group

D. Perspective

## ✅ Answer

**B**

### Explanation

Hierarchies allow users to drill naturally through related levels.

---

# Question 8 – Keep Rows vs Remove Rows

A CSV contains 20 million transactions.

Only completed orders are needed.

When should you filter the rows?

A. After loading into the semantic model.

B. During report creation.

C. In Power Query before loading.

D. Using a DAX measure.

## ✅ Answer

**C**

### Explanation

Removing unnecessary rows before loading reduces refresh time and semantic model size.

---

# Question 9 – Group By

A transaction table contains millions of individual sales.

Management only needs total sales by region.

Which Power Query transformation should you use?

A. Merge

B. Append

C. Group By

D. Split Column

## ✅ Answer

**C**

### Explanation

Group By aggregates detailed records before loading, reducing model size and improving performance.

---

# Question 10 – Split Column

A CustomerName column contains values such as:

```
John Smith
Maria Jones
```

The business wants separate FirstName and LastName columns.

Which transformation should you use?

A. Extract

B. Merge

C. Split Column

D. Pivot

## ✅ Answer

**C**

### Explanation

Split Column separates values based on a delimiter such as a space.

---

# ⭐ PL-300 Review

| Requirement | Best Feature |
|-------------|--------------|
| One visual ignores another | Edit Interactions |
| Hover for more information | Tooltip Page |
| Hide report pages | Hidden Pages |
| Correct map behavior | Data Category |
| Sort month names | Sort by Column |
| Prevent numeric aggregation | Don't Summarize |
| Easier drill-down | Hierarchy |
| Remove unnecessary records | Filter in Power Query |
| Aggregate before loading | Group By |
| Separate text values | Split Column |

# PL-300 Expert Practice Questions – Set 12
## Advanced Scenario Questions (Mixed PL-300 Objectives)

---

# Question 1 – Unpivot vs Pivot

A sales manager provides an Excel workbook containing the following data:

| Employee | Q1 | Q2 | Q3 | Q4 |
|-----------|----|----|----|----|
| Amy | 125 | 140 | 152 | 170 |
| Ben | 98 | 115 | 121 | 138 |

The business wants to create a line chart showing quarterly sales trends by employee.

What should you do first in Power Query?

A. Merge the table with another query.

B. Append the table.

C. Unpivot the quarter columns.

D. Pivot the Employee column.

## ✅ Answer

**C**

### Explanation

Charts require the quarter values to exist in a single column (Quarter) with a corresponding Sales value. Unpivot converts wide data into a normalized format suitable for visuals.

---

# Question 2 – Storage Mode

A semantic model contains:

- Sales (120 million rows)
- Product (25,000 rows)
- Customer (180,000 rows)

Sales data changes every few minutes.

This is a composite model.

Users frequently slice reports by Product and Customer and complain about slow filtering.

Which storage mode should be assigned to the Product and Customer tables?

A. Import

B. DirectQuery

C. Dual

D. Live Connection

## ✅ Answer

**C**

### Explanation

Dual storage mode allows dimension tables to behave as Import or DirectQuery depending on the query, improving performance in composite models.

---

# Question 3 – Tenant Settings

The Power BI administrator wants to prevent users from publishing reports publicly to the internet while continuing to allow internal sharing within the organization.

Which tenant setting should be disabled?

A. Export Data

B. Publish to web

C. Build Permission

D. XMLA Endpoint

## ✅ Answer

**B**

### Explanation

Disabling **Publish to web** prevents anonymous public access while preserving secure internal sharing.

---

# Question 4 – Dashboard Tiles

A report containing five visuals has already been published to the Power BI Service.

Management wants one visual displayed on an existing dashboard.

What should you do?

A. Open the report in the Service and pin the visual to the dashboard.

B. Publish the report again.

C. Export the report to PDF.

D. Create a bookmark.

## ✅ Answer

**A**

### Explanation

Dashboard tiles are created in the **Power BI Service** by pinning visuals from reports.

---

# Question 5 – CALCULATE + KEEPFILTERS

A report page includes a slicer for Product Category.

Management requests a measure that always filters to products priced above $100 **while still respecting the user's Product Category selection**.

Which DAX expression best meets the requirement?

A.

```DAX
CALCULATE(
    [Sales],
    Product[Price] > 100
)
```

B.

```DAX
CALCULATE(
    [Sales],
    KEEPFILTERS(Product[Price] > 100)
)
```

C.

```DAX
CALCULATE(
    [Sales],
    REMOVEFILTERS(Product)
)
```

D.

```DAX
SUM(Sales[SalesAmount])
```

## ✅ Answer

**B**

### Explanation

`KEEPFILTERS()` adds the price condition while preserving existing filters (such as Product Category) instead of replacing them.

---

# Question 6 – Remove Unwanted Columns

A SQL table contains 45 columns.

Only 12 are required for reporting.

What is the BEST approach?

A. Hide the unused columns.

B. Remove the columns in Power Query before loading.

C. Delete the columns after publishing.

D. Remove the columns using DAX.

## ✅ Answer

**B**

### Explanation

Removing unnecessary columns before loading reduces model size, refresh time, and memory usage.

---

# Question 7 – Paginated Reports

A finance department needs a report that:

- Prints perfectly on legal-size paper
- Contains thousands of invoice rows
- Requires exact page breaks and repeating headers

Which reporting solution should you recommend?

A. Dashboard

B. Standard Power BI Report

C. Paginated Report

D. Scorecard

## ✅ Answer

**C**

### Explanation

Paginated Reports are designed for highly formatted, printable, and pixel-perfect reports.

---

# Question 8 – Left Outer Join

You have:

**Sales**

- OrderID
- CustomerID

**Customers**

- CustomerID
- CustomerName

Management wants every sales record returned, even if a matching customer record does not exist.

Which join should you use?

A. Inner

B. Left Outer

C. Right Outer

D. Full Outer

## ✅ Answer

**B**

### Explanation

A Left Outer join keeps every row from the first (left) table and matches rows from the second table when available.

---

# Question 9 – PBIDS Files

A BI team wants business users to connect to the correct Power BI semantic model without manually entering connection information.

Which file type should they distribute?

A. PBIX

B. PBIDS

C. PBIT

D. CSV

## ✅ Answer

**B**

### Explanation

A **PBIDS** file stores connection information and opens Power BI Desktop connected to the specified data source.

---

# Question 10 – Dashboard Alerts

An executive wants to receive an email whenever daily sales exceed $500,000.

What should you configure?

A. Bookmark

B. Dashboard Data Alert

C. Drillthrough

D. Tooltip Page

## ✅ Answer

**B**

### Explanation

Data Alerts can be created on supported dashboard tiles in the Power BI Service and notify users when a KPI reaches a specified threshold.

---

# ⭐ Bonus Review (Rapid Fire)

| Requirement | Best Feature |
|-------------|--------------|
| Normalize month columns | Unpivot |
| Fast composite model filtering | Dual Storage Mode |
| Prevent public internet reports | Disable Publish to Web |
| Add report visual to dashboard | Pin Visual |
| Preserve existing filters in CALCULATE | KEEPFILTERS() |
| Reduce semantic model size | Remove Columns in Power Query |
| Printable invoices | Paginated Report |
| Keep all rows from first table | Left Outer Join |
| Preconfigured data connection | PBIDS |
| Email when KPI exceeds threshold | Dashboard Alert |

# PL-300 Expert Practice Questions – Set 13
## Advanced Scenario Questions (Mixed PL-300 Objectives)

---

# Question 1 – Fill Down

You import an Excel worksheet that was formatted for printing.

| Department | Employee | Salary |
|------------|----------|--------|
| Sales | John | 65,000 |
| *(blank)* | Mary | 72,000 |
| *(blank)* | Tim | 69,000 |
| HR | Susan | 81,000 |
| *(blank)* | David | 78,000 |

Every employee should inherit the department listed above them.

Which Power Query transformation should you use?

A. Replace Values

B. Fill Down

C. Merge Columns

D. Group By

## ✅ Answer

**B**

### Explanation

**Fill Down** copies the last non-blank value into subsequent blank rows, making it ideal for importing Excel reports designed for printing.

---

# Question 2 – Top N Filter

A report contains sales for 4,000 products.

Management wants to display **only the 15 products with the highest sales amount**, while allowing users to change Year and Region using slicers.

Which solution is BEST?

A. Filter the Product table in Power Query.

B. Apply a Top N visual filter using Total Sales.

C. Create a calculated column ranking the products.

D. Remove products outside the top 15 from the model.

## ✅ Answer

**B**

### Explanation

A **Top N visual filter** dynamically responds to slicers and displays the highest-ranking products based on a measure.

---

# Question 3 – Column Profile vs Distribution

A data analyst needs to identify:

- Minimum value
- Maximum value
- Average
- Standard deviation
- Number of distinct values

Which Power Query profiling feature should they use?

A. Column Quality

B. Column Distribution

C. Column Profile

D. Query Diagnostics

## ✅ Answer

**C**

### Explanation

**Column Profile** provides detailed statistics for the selected column, including min, max, average, distinct count, and value distribution.

---

# Question 4 – Outliers

A scatter chart displays customer spending.

Five customers have purchases over $10 million, while most customers spend less than $5,000.

The outliers make the remaining points appear compressed near the origin.

Management wants to minimize the visual impact of the outliers **without deleting any data**.

What is the BEST solution?

A. Delete the outlier records.

B. Apply a visual-level filter to exclude the outliers.

C. Use a logarithmic scale (if appropriate for the visual and analysis).

D. Convert the scatter chart to a pie chart.

## ✅ Answer

**C**

### Explanation

When supported and appropriate, a logarithmic scale reduces the visual dominance of extreme values while preserving all data. If a log scale isn't suitable for the chosen visual, other techniques may be needed, but the goal is to preserve the data.

---

# Question 5 – Sensitivity Labels

A report contains employee salaries.

The organization uses Microsoft Purview sensitivity labels.

The report should automatically inherit organizational protection policies when shared.

What should you apply?

A. Certified endorsement

B. Promoted endorsement

C. Sensitivity Label

D. Build Permission

## ✅ Answer

**C**

### Explanation

Sensitivity Labels classify and protect sensitive content and integrate with Microsoft Purview protection policies.

---

# Question 6 – Merge vs Append

A retail company receives:

- One table containing Products
- One table containing Suppliers

Each product has one SupplierID.

The business wants the supplier name added to every product.

Which Power Query transformation should you use?

A. Append

B. Merge

C. Pivot

D. Unpivot

## ✅ Answer

**B**

### Explanation

Merge combines related tables using matching keys. Append stacks rows from tables with the same structure.

---

# Question 7 – Workspace Roles

A user should:

- Publish reports
- Update semantic models
- Create dashboards

The user should **not** be able to add or remove workspace members.

Which workspace role is MOST appropriate?

A. Viewer

B. Contributor

C. Member

D. Admin

## ✅ Answer

**B**

### Explanation

A **Contributer** can publish, edit, and manage content but cannot manage workspace access like an Admin.

---

# Question 8 – Dashboard Mobile Layout

An executive reports that dashboard tiles appear in an inconvenient order on their phone.

You need to optimize the mobile experience.

What should you do?

A. Resize the report page.

B. Edit the dashboard's Mobile Layout in the Power BI Service.

C. Create a phone layout in Power BI Desktop.

D. Enable Responsive visuals.

## ✅ Answer

**B**

### Explanation

Dashboard mobile layouts are configured **in the Power BI Service**. (Phone layouts in Power BI Desktop apply to reports, not dashboards.)

---

# Question 9 – Sync Slicers

A report contains six pages.

A Date slicer should maintain the same selection across every page, but the slicer itself should only appear on two pages.

Which feature should you use?

A. Duplicate the slicer.

B. Sync Slicers and hide the slicer on selected pages.

C. Bookmarks.

D. Drillthrough.

## ✅ Answer

**B**

### Explanation

Sync Slicers allows filter selections to stay synchronized across report pages while controlling where the slicer is visible.

---

# Question 10 – Suitable Visual

Management wants to compare:

- Actual Sales
- Target Sales

for every sales region.

The report should clearly show regions that exceeded or fell short of their targets.

Which visual is MOST appropriate?

A. Pie Chart

B. Gauge

C. Clustered Column Chart

D. Scatter Chart

## ✅ Answer

**C**

### Explanation

A **Clustered Column Chart** allows users to compare Actual versus Target across multiple categories. A Gauge is better suited for showing progress toward a target for a single measure or a small number of KPIs.

---

# ⭐ PL-300 Quick Review

| Requirement | Best Solution |
|--------------|---------------|
| Fill blank values from above | Fill Down |
| Dynamic Top 15 products | Top N Visual Filter |
| Detailed column statistics | Column Profile |
| Reduce impact of outliers | Logarithmic scale (when appropriate) |
| Protect confidential reports | Sensitivity Label |
| Combine related tables | Merge |
| Publish content without managing users | Member |
| Arrange dashboard for phones | Dashboard Mobile Layout |
| Same slicer selection across pages | Sync Slicers |
| Compare Actual vs Target by category | Clustered Column Chart |

---

## 🚨 PL-300 Exam Traps

| Microsoft Says... | They're Testing... |
|-------------------|--------------------|
| "Rows inherit the value above" | Fill Down |
| "Highest 10/15/20 records" | Top N filter |
| "Detailed statistics" | Column Profile |
| "Protect sensitive data" | Sensitivity Labels |
| "Optimize dashboard on phones" | Dashboard Mobile Layout |
| "Same filter across report pages" | Sync Slicers |
| "Compare two measures across categories" | Clustered Column Chart |
| "Add columns from another table" | Merge |

# PL-300 Expert Practice Questions – Set 14
## Advanced Microsoft Exam-Style Scenarios (Mixed Topics)

These questions are written to resemble the reasoning style used on the PL-300 exam. More than one answer may seem reasonable, but only **one is the BEST answer.**

---

# Question 1 – Append vs Merge

A company stores sales transactions in separate yearly tables:

- Sales2023
- Sales2024
- Sales2025

Each table contains identical columns.

Management wants one report that analyzes sales across all three years.

What should you do?

A. Merge the three queries.

B. Append the three queries.

C. Create relationships between the three tables.

D. Create calculated columns that combine the tables.

## ✅ Answer

**B**

### Explanation

Appending combines rows from tables with the same structure. Merge is used when combining columns from related tables.

---

# Question 2 – Column Distribution

A developer notices duplicate customer IDs in a CSV file.

Which Power Query feature is the BEST choice to quickly determine how frequently each CustomerID appears?

A. Column Quality

B. Column Distribution

C. Column Profile

D. Query Dependencies

## ✅ Answer

**B**

### Explanation

Column Distribution displays distinct values and their frequency, making duplicate values easy to identify.

---

# Question 3 – Dashboard Tiles

A dashboard already contains a pinned KPI visual.

The underlying report visual is modified to display profit instead of revenue.

What happens to the dashboard tile?

A. The tile automatically reflects the updated visual after the report is republished.

B. The dashboard tile must be recreated.

C. The dashboard becomes disconnected.

D. Dashboard tiles never update.

## ✅ Answer

**A**

### Explanation

Dashboard tiles remain linked to the report visual. Once the updated report is published, the tile reflects the changes.

---

# Question 4 – Dashboard Alerts

A manager wants to receive an email notification whenever inventory falls **below** 100 units.

Which object can support a data alert?

A. A report visual in Power BI Desktop

B. A dashboard tile based on a supported visual

C. A Matrix visual

D. A paginated report

## ✅ Answer

**B**

### Explanation

Data alerts are configured on supported dashboard tiles in the Power BI Service, not directly on report visuals.

---

# Question 5 – Edit Interactions

A report contains:

- Matrix
- Slicer
- Stacked Column Chart

Selecting a row in the Matrix should **highlight** the chart instead of filtering it.

What should you configure?

A. Sync Slicers

B. Edit Interactions

C. Drillthrough

D. Cross-report filtering

## ✅ Answer

**B**

### Explanation

Edit Interactions allows you to choose whether visuals filter, highlight, or ignore one another.

---

# Question 6 – Suitable Visual

Management wants to display:

- Revenue
- Expenses
- Profit

for each department in a single comparison.

Which visual is MOST appropriate?

A. Pie Chart

B. Clustered Bar Chart

C. KPI

D. Gauge

## ✅ Answer

**B**

### Explanation

A clustered bar (or clustered column) chart is ideal for comparing multiple measures across categories.

---

# Question 7 – Paginated Reports

A regulatory agency requires a report that:

- Always prints exactly 50 rows per page
- Includes page numbers
- Repeats column headers on every page

Which reporting option should you choose?

A. Power BI Report

B. Dashboard

C. Paginated Report

D. Scorecard

## ✅ Answer

**C**

### Explanation

Paginated Reports are designed for precise printing, page control, and large tabular reports.

---

# Question 8 – Top N

A sales report should always display the **Top 20 Customers by Revenue**, regardless of how many customers exist in the dataset.

What is the BEST approach?

A. Filter the source data in Power Query.

B. Use a Top N visual filter based on the Revenue measure.

C. Delete customers outside the top 20.

D. Create a relationship to a ranking table.

## ✅ Answer

**B**

### Explanation

Top N visual filters dynamically calculate rankings based on the current filter context.

---

# Question 9 – Column Quality

A developer wants to quickly identify:

- Error values
- Empty values
- Valid values

Which profiling tool should be used?

A. Column Profile

B. Column Quality

C. Column Distribution

D. Query Diagnostics

## ✅ Answer

**B**

### Explanation

Column Quality provides percentages of valid, empty, and error values for each column.

---

# Question 10 – Workspace Permissions vs Report Sharing

A user has **Viewer** access to a workspace.

The report owner shares a report directly with the user.

The user can open the report but cannot create a new report from the semantic model.

What additional permission is required?

A. Member

B. Build

C. Admin

D. Contributor

## ✅ Answer

**B**

### Explanation

Sharing a report allows the user to view it. Creating new reports from the underlying semantic model requires **Build** permission.

---

# ⭐ PL-300 Quick Review

| Requirement | Correct Solution |
|-------------|------------------|
| Combine yearly transaction tables | Append |
| Find duplicate values | Column Distribution |
| Update dashboard tile | Republish updated report |
| Email notification on KPI | Dashboard Alert |
| Change filter/highlight behavior | Edit Interactions |
| Compare several measures by category | Clustered Bar/Column Chart |
| Pixel-perfect printed reports | Paginated Report |
| Highest N records | Top N Filter |
| Find errors and blanks | Column Quality |
| Create reports from a shared semantic model | Build Permission |

---

## 🚨 Microsoft Exam Tips

**Append vs Merge**

- Same columns → **Append**
- Related tables → **Merge**

**Power Query Profiling**

- **Column Quality** → Errors, Empty, Valid
- **Column Distribution** → Frequency, Distinct Values
- **Column Profile** → Full statistics (min, max, average, distinct count)

**Desktop vs Service**

- Dashboard Alerts → **Service**
- Pin Dashboard Tiles → **Service**
- Paginated Reports → Published and consumed through the Service
- Power Query transformations → **Desktop**



# PL-300 Expert Practice Questions – Set 15
## Advanced Mixed Scenarios

These questions are written to closely resemble the reasoning style used on the PL-300 exam. Read each business requirement carefully and choose the **BEST** solution.

---

# Question 1 – Data Reduction

A semantic model contains 45 million sales records.

A report page contains a scatter chart displaying every individual sale.

Users report that the visual is slow and difficult to interpret.

You need to improve report performance while still allowing users to identify sales trends.

What should you do?

A. Replace the scatter chart with a table.

B. Aggregate the data before displaying it in the visual.

C. Change the storage mode to DirectQuery.

D. Increase the canvas size.

## ✅ Answer

**B**

### Explanation

Displaying millions of individual points provides little analytical value. Aggregating the data (for example by month, region, or product) improves both readability and performance.

---

# Question 2 – Merge Join Types

You have two tables:

**Orders**

Contains every customer order.

**Returns**

Contains only returned orders.

Management wants a report showing every order, with return information when available.

Which join should be used?

A. Inner

B. Left Anti

C. Left Outer

D. Full Outer

## ✅ Answer

**C**

### Explanation

A Left Outer join keeps every order while matching return information when it exists.

---

# Question 3 – Left Anti Join

A company wants to identify customers who **have never placed an order**.

You have:

Customers

Orders

Which Merge Join should you use?

A. Inner

B. Left Outer

C. Left Anti

D. Right Outer

## ✅ Answer

**C**

### Explanation

A Left Anti join returns rows from the first table that have **no matching rows** in the second table.

---

# Question 4 – DAX Filter Context

Management requests a measure that returns Sales for only the **Bikes** category.

If users filter another category, the measure should still only calculate Bikes sales.

Which expression is BEST?

A.

```DAX
CALCULATE(
    [Sales],
    Product[Category]="Bikes"
)
```

B.

```DAX
SUM(Sales[SalesAmount])
```

C.

```DAX
AVERAGE(Sales[SalesAmount])
```

D.

```DAX
TOTALYTD([Sales],Date[Date])
```

## ✅ Answer

**A**

### Explanation

`CALCULATE()` changes the filter context by applying a filter for Bikes, regardless of report selections.

---

# Question 5 – Query Dependencies

A Power Query solution contains 28 queries.

You need to understand which queries depend on other queries before making changes.

Which feature should you use?

A. Column Profile

B. Query Dependencies

C. Performance Analyzer

D. Data View

## ✅ Answer

**B**

### Explanation

Query Dependencies provides a visual map showing relationships between Power Query queries.

---

# Question 6 – Import vs DirectQuery

A company stores inventory in SQL Server.

Inventory changes every 15 seconds.

Executives require reports showing nearly real-time inventory.

Which storage mode is MOST appropriate?

A. Import

B. DirectQuery

C. Dual

D. Live Connection

## ✅ Answer

**B**

### Explanation

DirectQuery retrieves data from the source during query execution, making it appropriate for near real-time reporting.

---

# Question 7 – Suitable Visual

Management wants to compare:

- Budget
- Actual

across 40 departments.

Users should immediately see which departments exceeded budget.

Which visual is BEST?

A. Pie Chart

B. Clustered Bar Chart

C. Gauge

D. Card

## ✅ Answer

**B**

### Explanation

Clustered bar charts are effective for comparing multiple measures across many categories.

---

# Question 8 – PBIX vs PBIT vs PBIDS

A consulting company wants to distribute a Power BI file that contains:

- Report layout
- Measures
- Queries

but **no imported data**.

Which file should they provide?

A. PBIX

B. PBIDS

C. PBIT

D. CSV

## ✅ Answer

**C**

### Explanation

A **PBIT** (Power BI Template) stores the report definition without the imported data, making it ideal for reusable templates.

---

# Question 9 – Report Accessibility

A report relies heavily on red and green colors to indicate performance.

The organization wants the report to be accessible to users with color vision deficiencies.

Which solution BEST meets the requirement?

A. Increase font sizes.

B. Add icons or shapes in addition to color.

C. Replace the report with a table.

D. Remove conditional formatting.

## ✅ Answer

**B**

### Explanation

Color alone should not communicate meaning. Icons, labels, or shapes improve accessibility for users with color vision deficiencies.

---

# Question 10 – Report Pages

A report contains:

- Executive Summary
- Sales Detail
- Customer Detail
- Inventory Detail

Executives should only navigate to the Executive Summary page, while analysts should be able to access every page.

What is the BEST solution?

A. Create four separate reports.

B. Hide the detailed pages before publishing the executive version of the report.

C. Duplicate every page.

D. Create four workspaces.

## ✅ Answer

**B**

### Explanation

Hidden pages provide a cleaner navigation experience while remaining available when appropriate. If different audiences require different content, separate reports or apps may also be appropriate, but for this requirement hiding the pages is the simplest solution.

---

# ⭐ PL-300 Quick Review

| Requirement | Best Solution |
|--------------|---------------|
| Millions of data points | Aggregate before visualizing |
| Keep all rows from first table | Left Outer Join |
| Find records without matches | Left Anti Join |
| Force a filter in a measure | CALCULATE() |
| Show query relationships | Query Dependencies |
| Near real-time reporting | DirectQuery |
| Compare Budget vs Actual | Clustered Bar/Column |
| Share report without data | PBIT |
| Accessibility | Icons + Color |
| Simplify report navigation | Hide Pages |

---

## 🚨 PL-300 Exam Traps

- **PBIX** = Report + Model + Data
- **PBIT** = Report + Model (No Data)
- **PBIDS** = Connection shortcut to a data source

- **Left Outer** = Keep all matches from the first table
- **Left Anti** = Return only rows with **no** match

- **Import** = Best performance
- **DirectQuery** = Most current data
- **Dual** = Optimizes composite models

- Don't rely on **color alone** to communicate information—Microsoft frequently tests accessibility best practices.