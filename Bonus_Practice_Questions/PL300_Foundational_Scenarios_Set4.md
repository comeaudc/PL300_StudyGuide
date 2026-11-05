# PL-300 Practice Questions: Foundational Scenarios — Set 4

**10 original, easier-range scenario-based multiple-choice questions with answers and explanations**

## Alignment with the current PL-300 exam

Checked against Microsoft's *Study guide for Exam PL-300: Microsoft Power BI Data Analyst*, skills measured as of **April 20, 2026**.

This set focuses on listed objectives: data source credentials and privacy levels; choosing Import or DirectQuery; creating parameters; pivoting data; configuring report interactions and slicers; choosing a distribution method; and identifying when a gateway is required.

These are original practice questions, not actual Microsoft exam questions. Microsoft notes that related topics may also be tested.

Official study guide: https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/pl-300

---

## 1. Data Source Settings: Credentials

An analyst opens a Power BI report connected to a company database. Refresh fails because the saved database credentials have expired. Where should the analyst start troubleshooting?

A. The visual's conditional formatting settings  
B. Data source settings, to update the credentials  
C. The report's drillthrough page  
D. The Selection pane

**Answer: B. Data source settings, to update the credentials.**

**Explanation:** PL-300 includes changing data source settings, including credentials. Expired or incorrect credentials can prevent Power BI from accessing the source during refresh.

## 2. Data Privacy Levels

An analyst combines data from a private company database with data from a public web source in Power Query. Power Query displays a privacy-level warning. What should the analyst do?

A. Set every source to Public without checking the source's sensitivity.  
B. Review and configure the appropriate privacy levels for the sources.  
C. Delete all relationships in the model.  
D. Replace all Power Query steps with DAX measures.

**Answer: B. Review and configure the appropriate privacy levels for the sources.**

**Explanation:** Privacy levels help control how data from different sources may be combined. Choose levels that reflect the sensitivity and intended sharing of each source, rather than disabling safeguards indiscriminately.

## 3. Choose a Storage Mode: Import

A sales dataset is small enough to fit comfortably in the Power BI model. Users want fast report interactions, and the business can refresh the data on a schedule rather than requiring every query to go directly to the source. Which storage mode is generally the best fit?

A. Import  
B. DirectQuery  
C. A report tooltip  
D. A workspace role

**Answer: A. Import.**

**Explanation:** Import loads data into the semantic model, which generally provides fast interactive analysis. The model must be refreshed to receive updated source data.

## 4. Choose a Storage Mode: DirectQuery

A business has a very large database table and requires report queries to use current data from the source. The model should not import the full table into Power BI. Which storage mode is the most likely fit?

A. Import  
B. DirectQuery  
C. Export to PDF  
D. A calculated column

**Answer: B. DirectQuery.**

**Explanation:** DirectQuery leaves data in the source and sends queries to it as users interact with the report. Performance and feature behavior depend on the source system and model design.

## 5. Power Query: Parameters

A report is developed against a test database. Before deployment, the analyst wants to switch the server or database name without manually editing several query steps. What Power Query feature can help?

A. A parameter  
B. A bookmark  
C. A drillthrough filter  
D. A DAX hierarchy

**Answer: A. A parameter.**

**Explanation:** Parameters store reusable values that can be referenced by queries, such as a server name, database name, folder path, or date boundary. Updating the parameter can make it easier to switch environments.

## 6. Power Query: Pivot Columns

A source table has three columns: `Region`, `Month`, and `Sales`. Each region has a row for each month. The analyst wants each month to become its own column, with sales values in the cells. Which Power Query operation should they use?

A. Append  
B. Pivot Column  
C. Unpivot Columns  
D. Merge Queries

**Answer: B. Pivot Column.**

**Explanation:** Pivot turns values from one column—in this case, Month—into separate columns. Unpivot does the reverse, turning multiple columns into attribute-value rows.

## 7. Report Interactions

A report page contains a bar chart of sales by region and a table of individual orders. When a user selects one region in the bar chart, the table is filtered to show orders from that region. Which Power BI feature controls this behavior?

A. Edit interactions  
B. Data source credentials  
C. Power Query parameters  
D. Workspace sensitivity labels

**Answer: A. Edit interactions.**

**Explanation:** Visual interactions determine whether selecting data in one visual filters, highlights, or has no effect on another visual. Use Edit interactions to configure the behavior.

## 8. Sync Slicers

A report has three pages, each showing sales information. Users want one Year slicer selection to apply consistently across all three pages. Which feature should the analyst configure?

A. Sync slicers  
B. Column Quality  
C. Append Queries  
D. Row-level security

**Answer: A. Sync slicers.**

**Explanation:** Sync slicers lets a slicer selection apply across multiple report pages. Visibility can also be configured separately from synchronization.

## 9. Refresh: On-Premises Data Gateway

A Power BI semantic model uses data stored in a database on a company's on-premises network. The model is published to the Power BI service, and scheduled refresh must access that database. What may be required?

A. An on-premises data gateway configured with appropriate data-source access  
B. A new report page for every refresh  
C. A DAX measure named `Refresh`  
D. A bookmark that stores the database password

**Answer: A. An on-premises data gateway configured with appropriate data-source access.**

**Explanation:** A gateway commonly enables the Power BI service to securely reach supported on-premises data sources for refresh or queries. The exact requirement depends on the source and connectivity setup.

## 10. Distributing Reports: App or Workspace Access

A team wants to distribute a curated collection of Power BI reports and dashboards to a broad audience of business users, without giving all consumers workspace editing permissions. Which distribution approach is generally designed for this?

A. Publish a Power BI app from the workspace  
B. Make every consumer a workspace Admin  
C. Send each user the source CSV files only  
D. Create a separate tenant for every consumer

**Answer: A. Publish a Power BI app from the workspace.**

**Explanation:** A Power BI app provides a packaged way to distribute curated content to consumers. Workspace roles are intended for collaboration and management; consumers generally do not need Admin or editing permissions just to view distributed content.

---

## Quick Review

| Topic | Key point |
|---|---|
| **Credentials** | Update data source credentials when access or refresh fails because they are invalid or expired |
| **Privacy levels** | Set levels that reflect how sensitive sources should be handled when combined |
| **Import** | Loads data into the semantic model; refresh updates it |
| **DirectQuery** | Queries the source as needed rather than importing the full data |
| **Parameters** | Store reusable values such as server names or file paths |
| **Pivot** | Turns values in a column into separate columns |
| **Edit interactions** | Controls how visuals affect other visuals |
| **Sync slicers** | Shares slicer selections across report pages |
| **Gateway** | Can connect the Power BI service to supported on-premises sources |
| **Power BI app** | Distributes curated content to consumers without requiring workspace editing access |

## Source

Microsoft Learn, [Study guide for Exam PL-300: Microsoft Power BI Data Analyst](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/pl-300) — skills measured as of April 20, 2026.
