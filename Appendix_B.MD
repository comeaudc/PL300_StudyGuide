# Appendix B — PL-300 Exam Cheat Sheets

## Microsoft Power BI Data Analyst Associate (PL-300)

---

# B.1 Top 50 PL-300 Concepts You Must Know

These are the concepts that appear repeatedly on the PL-300 exam.

|  # | Concept                    | Know This                                        |
| -: | -------------------------- | ------------------------------------------------ |
|  1 | Power Query                | Used before data is loaded                       |
|  2 | DAX                        | Used after data is loaded                        |
|  3 | Import Mode                | Fastest performance for most reports             |
|  4 | DirectQuery                | Queries source at runtime                        |
|  5 | Dual Storage               | Usually for dimension tables in composite models |
|  6 | Live Connection            | Connects to an existing semantic model           |
|  7 | Semantic Model             | Contains tables, relationships, and DAX          |
|  8 | Star Schema                | Preferred model design                           |
|  9 | Fact Table                 | Transactions and numeric values                  |
| 10 | Dimension Table            | Descriptive attributes                           |
| 11 | One-to-Many                | Most common relationship                         |
| 12 | Single Direction Filtering | Default and recommended                          |
| 13 | Many-to-Many               | Use only when necessary                          |
| 14 | Active Relationship        | Used automatically                               |
| 15 | Inactive Relationship      | Requires USERELATIONSHIP()                       |
| 16 | Date Table                 | Required for robust time intelligence            |
| 17 | Measures                   | Dynamic calculations                             |
| 18 | Calculated Columns         | Stored row-level calculations                    |
| 19 | Calculated Tables          | Created using DAX                                |
| 20 | CALCULATE()                | Changes filter context                           |
| 21 | SUMX()                     | Iterator function                                |
| 22 | ALL()                      | Removes filters                                  |
| 23 | REMOVEFILTERS()            | Removes filters (clear intent)                   |
| 24 | VALUES()                   | Returns unique values (may include blank)        |
| 25 | Variables (VAR)            | Improve readability and maintainability          |
| 26 | Query Folding              | Pushes transformations to the source             |
| 27 | Merge                      | Join tables (columns)                            |
| 28 | Append                     | Combine tables (rows)                            |
| 29 | Reference Query            | Depends on original query                        |
| 30 | Duplicate Query            | Independent copy                                 |
| 31 | Column Quality/Profile     | Data profiling tools                             |
| 32 | Incremental Refresh        | Refresh only changed partitions                  |
| 33 | Drill Down                 | Navigate hierarchy in the same visual            |
| 34 | Drillthrough               | Navigate to another report page                  |
| 35 | Bookmarks                  | Save report state                                |
| 36 | Sync Slicers               | Synchronize slicers across report pages          |
| 37 | Conditional Formatting     | Highlight values visually                        |
| 38 | Key Influencers            | Find factors affecting a result                  |
| 39 | Decomposition Tree         | Investigate a measure interactively              |
| 40 | Q&A                        | Natural language querying                        |
| 41 | Performance Analyzer       | Identify report bottlenecks                      |
| 42 | Workspace                  | Collaboration area                               |
| 43 | App                        | Distribute finished content                      |
| 44 | Build Permission           | Create reports from a semantic model             |
| 45 | RLS                        | Restrict data by user                            |
| 46 | Gateway                    | Connect Power BI Service to on-premises data     |
| 47 | Scheduled Refresh          | Update imported datasets automatically           |
| 48 | Tenant Settings            | Organization-wide Power BI configuration         |
| 49 | Promoted vs Certified      | Levels of content endorsement                    |
| 50 | Workspace Roles            | Viewer, Contributor, Member, Admin               |

---

# B.2 Microsoft Question Wording → What They Are Really Asking

| If the question says...                 | Think...                       |
| --------------------------------------- | ------------------------------ |
| "Clean the data before loading."        | Power Query                    |
| "Users need current data."              | DirectQuery                    |
| "Users need the fastest reports."       | Import                         |
| "Combine rows from multiple files."     | Append                         |
| "Add columns from another table."       | Merge                          |
| "Only changed data should refresh."     | Incremental Refresh            |
| "Dynamic calculation based on slicers." | Measure                        |
| "One value for every row."              | Calculated Column              |
| "Compare this year to last year."       | Time Intelligence + Date Table |
| "Restrict users to their region."       | RLS                            |
| "Users create reports from a dataset."  | Build permission               |
| "Investigate why sales dropped."        | Decomposition Tree             |
| "Find what influences churn."           | Key Influencers                |
| "User wants to type questions."         | Q&A                            |
| "Move to a detail page."                | Drillthrough                   |
| "Expand Year → Quarter → Month."        | Drill Down                     |
| "Hide/show visuals with a button."      | Bookmark                       |
| "Same slicer on multiple pages."        | Sync Slicers                   |
| "Distribute finished reports."          | App                            |
| "Collaborate on reports."               | Workspace                      |

---

# B.3 The 25 Most Common PL-300 Distractors

These are the traps Microsoft likes to use.

| Incorrect Assumption                          | Correct Understanding                                       |
| --------------------------------------------- | ----------------------------------------------------------- |
| DirectQuery is always faster.                 | Import is usually faster.                                   |
| Measures are calculated during refresh.       | Measures calculate at query time.                           |
| Calculated columns react to slicers.          | They are evaluated during refresh.                          |
| Merge and Append do the same thing.           | Merge = columns, Append = rows.                             |
| Drill Down and Drillthrough are identical.    | They solve different problems.                              |
| Contributor can publish apps.                 | Only Members and Admins can publish/update apps.            |
| Viewer can create reports.                    | Requires Build permission and access to the semantic model. |
| RLS affects workspace Admins.                 | Workspace editors bypass RLS.                               |
| Gateway is required for every refresh.        | Generally only for on-premises data sources.                |
| Power Query and DAX are interchangeable.      | They solve different problems.                              |
| ALL() returns every row.                      | It removes filter context.                                  |
| SUM() and SUMX() are the same.                | SUMX evaluates an expression row by row.                    |
| Bidirectional filtering is recommended.       | Single direction is the default recommendation.             |
| Pie charts work well for many categories.     | Use with only a small number of categories.                 |
| Dashboards are created in Desktop.            | Dashboards are created in the Service.                      |
| Apps replace workspaces.                      | Apps distribute workspace content.                          |
| Bookmarks only save navigation.               | They save report state.                                     |
| Time intelligence works without a date table. | A proper date table is required.                            |
| Live Connection imports data.                 | It connects to an existing semantic model.                  |
| Build permission allows editing reports.      | It allows creating new reports from the model.              |
| Promoted = Certified.                         | Certified has stricter approval.                            |
| Reference and Duplicate are identical.        | Reference depends on the original query.                    |
| Query folding always occurs.                  | Some transformations break folding.                         |
| Performance Analyzer fixes reports.           | It identifies bottlenecks.                                  |
| Storage mode and connector are the same.      | They are different concepts.                                |

---

# B.4 Decision Trees

## Cleaning or Calculating?

```text
Need to clean data?

        │
        ├── Yes → Power Query
        │
        └── No
              │
              └── Need dynamic calculation?
                        │
                        ├── Yes → Measure
                        └── Row-level calculation → Calculated Column
```

---

## Merge or Append?

```text
Need more columns?

     │
     ├── Yes → Merge
     │
     └── No
            │
            └── Need more rows?
                    │
                    └── Append
```

---

## Storage Mode

```text
Need fastest performance?

      │
      ├── Yes → Import
      │
      └── Need near real-time data?
                │
                ├── Yes → DirectQuery
                │
                └── Composite Model?
                        │
                        └── Dual (typically for dimensions)
```

---

## Visual Selection

```text
Compare categories → Bar/Column

Trend over time → Line

Single KPI → Card

Relationship → Scatter

Drivers → Key Influencers

Investigate causes → Decomposition Tree

Detailed hierarchy → Matrix

Geography → Map
```

---

# B.5 DAX Cheat Sheet

## Measures vs Calculated Columns

| Measure             | Calculated Column                     |
| ------------------- | ------------------------------------- |
| Dynamic             | Stored                                |
| Uses filter context | Uses row context                      |
| Preferred for KPIs  | Preferred for row-by-row calculations |

---

## Core Functions

| Function        | Purpose                          |
| --------------- | -------------------------------- |
| SUM()           | Add a column                     |
| SUMX()          | Add calculated values row by row |
| COUNTROWS()     | Count table rows                 |
| DISTINCTCOUNT() | Count unique values              |
| CALCULATE()     | Modify filter context            |
| ALL()           | Remove filters                   |
| REMOVEFILTERS() | Clear filters                    |
| VALUES()        | Return unique values             |
| DIVIDE()        | Safe division                    |

---

## Context Reminder

Row Context

→ Calculated Columns

→ Iterators

Filter Context

→ Measures

→ Slicers

→ Filters

---

# B.6 Power Query Cheat Sheet

Always perform these tasks in Power Query whenever possible:

* Remove unnecessary columns
* Filter unwanted rows
* Correct data types
* Split or merge columns
* Replace errors
* Remove duplicates
* Merge tables
* Append tables
* Create conditional columns
* Use query folding when available

---

# B.7 Security Cheat Sheet

## Workspace Roles

| Role        | Typical Use                        |
| ----------- | ---------------------------------- |
| Viewer      | Consume content                    |
| Contributor | Create and publish reports/content |
| Member      | Manage content and publish apps    |
| Admin       | Full workspace control             |

---

## Permissions

| Permission | Purpose                              |
| ---------- | ------------------------------------ |
| Read       | View content                         |
| Build      | Create reports from a semantic model |

---

## Row-Level Security

Remember:

* Created in Desktop
* Assigned in Service
* Filters data for consumers
* Workspace editors generally bypass RLS

---

# B.8 Last Week Before the Exam

## 7 Days Before

Review:

* Storage modes
* Power Query
* Relationships
* Star schema

---

## 5 Days Before

Review:

* DAX
* CALCULATE()
* Measures vs Columns
* Time Intelligence

---

## 3 Days Before

Review:

* Visual selection
* AI visuals
* Drillthrough
* Bookmarks
* Sync slicers

---

## 2 Days Before

Review:

* Workspaces
* Apps
* RLS
* Gateways
* Build permission
* Workspace roles

---

## 1 Day Before

Complete:

* One full-length practice exam
* Review incorrect answers only
* Read Appendix A and Appendix B
* Avoid learning entirely new topics

---

# B.9 Exam Day Checklist

Before selecting an answer, ask yourself:

☐ Is this a Power Query problem or a DAX problem?

☐ Is this asking about Desktop or Service?

☐ Is the question testing storage mode?

☐ Is it asking for the fastest, simplest, or most maintainable solution?

☐ Does the business requirement mention security?

☐ Is there a workspace role involved?

☐ Is this about sharing or distributing content?

☐ Is there a better feature that more directly satisfies the requirement?

☐ Did I eliminate distractors before choosing?

---

# Final Advice

The PL-300 is designed to test **decision-making**, not memorization.

When solving a question:

1. Identify the business requirement.
2. Identify the Power BI feature that directly addresses it.
3. Eliminate answers that are technically possible but not the *best* solution.
4. Watch for subtle distinctions (for example, **Contributor vs. Member**, **Merge vs. Append**, or **Drill Down vs. Drillthrough**).

If you consistently think in terms of **requirement → feature → reason**, you'll be well prepared for the style of questions Microsoft uses on the exam.
