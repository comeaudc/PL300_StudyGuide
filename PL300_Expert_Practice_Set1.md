
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
