# PL-300 Practice Questions: Power BI Fundamentals

**10 easier-range, scenario-based multiple-choice questions with answers and explanations**

Topics: Power BI Desktop vs. Power BI service, tenant and workspace concepts, Power Query Editor (PQE), and Power Query vs. DAX.

These are original practice questions based on common PL-300 skills, not actual Microsoft exam questions.

## 1. Power BI Desktop vs. Power BI Service

A data analyst needs to connect to a CSV file, clean the data, build relationships, create DAX measures, and design a report. Where should the analyst primarily do this work?

A. Power BI service  
B. Power BI Desktop  
C. Microsoft Teams only  
D. The Power BI admin portal

**Answer: B. Power BI Desktop.**

**Explanation:** Power BI Desktop is the primary authoring tool for connecting to data, transforming it, modeling it, writing DAX, and building reports. The report can then be published to the Power BI service for sharing and collaboration.

## 2. Power BI Service: Sharing a Report

An analyst has finished a report in Power BI Desktop and wants colleagues to view it online. Which action is the usual next step?

A. Publish the report to the Power BI service.  
B. Convert every measure into a Power Query step.  
C. Save the PBIX file only to the local desktop.  
D. Create a new Microsoft tenant for each colleague.

**Answer: A. Publish the report to the Power BI service.**

**Explanation:** Publishing sends the report and its semantic model to a workspace in the Power BI service, where access and collaboration can be managed.

## 3. Power BI Service: Workspace Purpose

A team of analysts needs a shared place in the Power BI service to organize reports, dashboards, and semantic models and collaborate on content. What should they use?

A. A personal folder on one analyst's computer  
B. A workspace  
C. A DAX calculated column  
D. Power Query's Column Distribution pane

**Answer: B. A workspace.**

**Explanation:** Workspaces are collaborative areas in the Power BI service for organizing and managing Power BI content. Access is controlled through workspace roles and other permissions.

## 4. Tenant: Organization-Level Environment

A company uses Microsoft Power BI and Microsoft 365. An administrator manages organization-wide Power BI settings and controls which features users can access. What does the term **tenant** most closely refer to?

A. One report page  
B. The organization's environment in Microsoft's cloud, with its users and organization-level settings  
C. A single Power Query step  
D. One visual in a report

**Answer: B. The organization's environment in Microsoft's cloud, with its users and organization-level settings.**

**Explanation:** A tenant is the organization's environment in Microsoft's cloud. Tenant-level settings can govern how Power BI features are made available across the organization. A workspace is a smaller collaborative area within that environment.

## 5. Power Query Editor: Cleaning Data

An analyst imports an Excel table into Power BI. Before loading it, they need to remove blank rows, rename columns, split a full-name column, and correct data types. Where should they perform these tasks?

A. Power Query Editor  
B. The report filter pane only  
C. DAX measures  
D. The dashboard tile settings

**Answer: A. Power Query Editor.**

**Explanation:** Power Query Editor is used to connect to, clean, and transform data before it is loaded into the semantic model. The transformations are recorded as applied steps and can run again during refresh.

## 6. Power Query vs. DAX: Replace Invalid Text

A source column contains product prices stored as text, including some values such as `unknown`. The analyst needs to inspect and clean the values before they enter the model. Which tool is generally the best place to do this?

A. DAX, because DAX replaces all Power Query transformations  
B. Power Query Editor, to clean and convert the source values  
C. The report canvas, by changing the chart type  
D. Workspace roles

**Answer: B. Power Query Editor, to clean and convert the source values.**

**Explanation:** Power Query is generally used for data cleaning and shaping before loading. The analyst should decide how to handle invalid values, then convert the column to an appropriate numeric type. DAX is primarily used for model calculations.

## 7. Power Query vs. DAX: Dynamic Total

A report needs a total sales value that updates when a user selects a different year or region in a slicer. Which is generally the best choice?

A. A DAX measure  
B. A fixed value typed into Power Query  
C. A renamed column  
D. A tenant setting

**Answer: A. A DAX measure.**

**Explanation:** Measures are evaluated in the current filter context, so their results respond to slicers and report filters. Power Query transformations are normally performed when data is refreshed, not recalculated interactively for each slicer selection.

## 8. Power Query vs. DAX: Standardize Source Values

An analyst wants to standardize product labels by replacing `Cell Phone`, `cellphone`, and `Mobile` with the same category before the data is loaded into the model. Which approach is generally most appropriate?

A. Use Power Query transformations to standardize the source values.  
B. Create a separate report page for each spelling.  
C. Change the workspace role to Contributor.  
D. Use a DAX measure to rename the original text values in the source.

**Answer: A. Use Power Query transformations to standardize the source values.**

**Explanation:** Standardizing source values is a data-preparation task. Power Query can replace values or apply conditional logic before loading the cleaned data into the model.

## 9. Power BI Service: Workspace Roles

A team member needs to publish and manage content in a shared workspace, but should not be the workspace's administrator. Which workspace role is generally appropriate if they need to create, edit, and publish content but not manage access?

A. Viewer  
B. Contributor  
C. Read-only report consumer with no workspace role  
D. Tenant administrator

**Answer: B. Contributor.**

**Explanation:** The Contributor role generally allows users to create, edit, and publish workspace content without granting the same workspace-management permissions as Admin or Member. Exact capabilities can depend on the action and the organization's configuration.

## 10. Power Query vs. DAX: When Does It Run?

An analyst creates a Power Query step that removes rows where `Status = "Cancelled"`. A report consumer then changes a slicer from one year to another. When does the row-removal transformation normally run?

A. Every time the consumer changes the slicer  
B. During query evaluation/refresh, not each time a report slicer changes  
C. Only when a dashboard tile is clicked  
D. Only after a user changes a workspace role

**Answer: B. During query evaluation/refresh, not each time a report slicer changes.**

**Explanation:** Power Query transformations are applied as data is retrieved and refreshed. Slicers typically filter the already-loaded model interactively; they do not rerun the Power Query cleaning steps each time a selection changes.

---

## Quick Review

| Concept | Remember |
|---|---|
| **Power BI Desktop** | Connect, transform, model, write DAX, and author reports |
| **Power BI service** | Publish, share, collaborate, manage access, and consume content online |
| **Workspace** | Shared area for organizing and collaborating on Power BI content |
| **Tenant** | Organization-level Microsoft cloud environment and settings |
| **Power Query Editor** | Clean and transform data before it is loaded |
| **DAX measure** | Calculate values dynamically in the current report filter context |
| **Power Query refresh** | Reapplies data preparation steps as data is retrieved/refreshed |
| **Workspace Contributor** | Creates and edits content without being a workspace administrator |

## Instructor Tip

A useful rule of thumb for beginners:

- **Power Query:** “Shape the data before it enters the model.”
- **DAX:** “Calculate values from the data in the model.”
- **Desktop:** “Build the report and model.”
- **Service:** “Publish, share, collaborate, and manage content.”
- **Tenant:** “Organization-level environment and controls.”
- **Workspace:** “Shared place for a team's Power BI content.”
