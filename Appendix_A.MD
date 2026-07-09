# Appendix A — PL-300 Quick Reference Tables

## Microsoft Power BI Data Analyst Associate (PL-300)

---

# A.1 Power BI Storage Modes Comparison

Storage mode questions are common because Microsoft tests **when and why** each mode should be used.

| Feature                 | Import              | DirectQuery       | Dual             | Live Connection          |
| ----------------------- | ------------------- | ----------------- | ---------------- | ------------------------ |
| Data stored in Power BI | Yes                 | No                | Partially        | No                       |
| Data stored in source   | Yes                 | Yes               | Yes              | Yes                      |
| Fast report performance | Excellent           | Depends on source | Excellent        | Depends                  |
| Requires refresh        | Yes                 | No                | Depends          | No                       |
| Supports DAX            | Full                | Some limitations  | Full             | Limited                  |
| Works with large data   | Limited by capacity | Excellent         | Excellent        | Excellent                |
| Common use              | Most reports        | Real-time data    | Composite models | Existing semantic models |

---

## When to Choose Each

### Import

Choose when:

✅ Data does not need real-time updates
✅ Performance is important
✅ Dataset fits capacity limits

Example:

Daily sales reporting.

---

### DirectQuery

Choose when:

✅ Data is very large
✅ Data must remain in source
✅ Near real-time reporting is required

Example:

Live operational dashboard.

---

### Dual

Choose when:

✅ Using Composite Models
✅ Dimension tables need flexibility

Example:

Customer/Product tables connected to Import and DirectQuery facts.

---

### Live Connection

Choose when:

✅ Connecting to an existing semantic model
✅ Centralized enterprise model already exists

Example:

Corporate finance model.

---

# PL-300 Trap

❌ DirectQuery is always faster because data is not imported.

Correct:

Import is usually faster because data is stored in memory.

---

---

# A.2 Power Query vs DAX Decision Guide

This is one of the most important PL-300 concepts.

| Requirement                     | Use         |
| ------------------------------- | ----------- |
| Clean messy data                | Power Query |
| Remove duplicates               | Power Query |
| Change data types               | Power Query |
| Combine files                   | Power Query |
| Merge tables before loading     | Power Query |
| Create reusable transformations | Power Query |
| Create dynamic calculations     | DAX         |
| Create KPIs                     | DAX         |
| Calculate percentages           | DAX         |
| Time intelligence               | DAX         |

---

# Rule

Ask:

"Does this need to happen before data enters the model?"

If yes:

✅ Power Query

If no:

✅ DAX

---

# Example

Need:

Remove invalid sales records.

Answer:

Power Query

---

Need:

Calculate profit margin by selected month.

Answer:

DAX Measure

---

---

# A.3 Merge vs Append

| Feature                  | Merge              | Append             |
| ------------------------ | ------------------ | ------------------ |
| Combines                 | Columns            | Rows               |
| Similar to SQL           | JOIN               | UNION              |
| Requires matching column | Yes                | Yes                |
| Used for                 | Adding information | Combining datasets |

---

# Merge Example

Customer table:

CustomerID

*

Customer Details:

CustomerID

Result:

More columns.

---

# Append Example

Sales 2025

*

Sales 2026

Result:

More rows.

---

# PL-300 Trap

Question:

"Combine January, February, and March sales files."

Answer:

✅ Append

---

---

# A.4 Reference vs Duplicate Queries

| Feature                 | Reference | Duplicate |
| ----------------------- | --------- | --------- |
| Creates copy            | No        | Yes       |
| Depends on original     | Yes       | No        |
| Updates with original   | Yes       | No        |
| Best for reusable logic | Yes       | Sometimes |

---

# Reference Example

Create:

Clean Sales Query

Then create:

Sales Summary

from it.

---

# Duplicate Example

Create an independent version.

---

# PL-300 Rule

Reference maintains a relationship.

Duplicate creates a separate query.

---

---

# A.5 Relationships Quick Guide

| Relationship | Meaning            |
| ------------ | ------------------ |
| One-to-many  | Most common        |
| Many-to-many | Advanced scenarios |
| One-to-one   | Rare               |

---

# Recommended Model

Star Schema:

```
        Date
          |
Customer - Sales - Product
          |
       Geography
```

---

# Fact Tables

Contain:

* Transactions
* Measurements
* Numbers

Example:

Sales

---

# Dimension Tables

Contain:

* Descriptions
* Categories
* Attributes

Example:

Customer

---

# A.6 Filter Direction

| Direction | Use                 |
| --------- | ------------------- |
| Single    | Recommended default |
| Both      | Special scenarios   |

---

# Bidirectional Filtering Risks

Can cause:

* Ambiguous relationships
* Performance problems

---

# PL-300 Rule

Use single direction unless requirements require otherwise.

---

---

# A.7 Measures vs Calculated Columns

| Feature    | Measure    | Calculated Column    |
| ---------- | ---------- | -------------------- |
| Calculated | Query time | Refresh time         |
| Storage    | Minimal    | Increases model size |
| Context    | Filter     | Row                  |
| Best for   | Analysis   | Row calculations     |

---

# Use Measure

Example:

Total Revenue

---

# Use Column

Example:

Profit per transaction

---

---

# A.8 DAX Context Reference

## Row Context

"The current row"

Common with:

* Calculated columns
* Iterators

---

## Filter Context

"Filters applied to the calculation"

Created by:

* Slicers
* Filters
* Visuals

---

## CALCULATE()

Changes filter context.

---

# PL-300 Rule

If the question says:

"Change filters"

Think:

CALCULATE()

---

---

# A.9 Visual Selection Guide

| Business Question   | Visual             |
| ------------------- | ------------------ |
| Compare categories  | Bar chart          |
| Show trends         | Line chart         |
| Show KPI            | Card               |
| Show relationships  | Scatter            |
| Geographic analysis | Map                |
| Explain drivers     | Key Influencers    |
| Explore causes      | Decomposition Tree |
| Detailed hierarchy  | Matrix             |

---

# A.10 Drill Down vs Drillthrough

| Feature  | Drill Down  | Drillthrough       |
| -------- | ----------- | ------------------ |
| Location | Same visual | Different page     |
| Requires | Hierarchy   | Drillthrough field |
| Purpose  | More detail | Detailed analysis  |

---

# Example

Year → Month:

Drill Down

---

Sales Summary → Customer Details:

Drillthrough

---

---

# A.11 Gateway Decision Guide

| Situation          | Gateway Needed |
| ------------------ | -------------- |
| Local SQL Server   | Yes            |
| On-prem File Share | Yes            |
| Azure SQL          | Usually No     |
| SharePoint Online  | No             |
| Power BI Dataset   | No             |

---

# Gateway Purpose

Connect:

On-premises data

↓

Power BI Service

---

---

# A.12 Workspace Roles Quick Reference

| Ability         | Viewer | Contributor | Member  | Admin |
| --------------- | ------ | ----------- | ------- | ----- |
| View content    | ✅      | ✅           | ✅       | ✅     |
| Create reports  | ❌      | ✅           | ✅       | ✅     |
| Publish reports | ❌      | ✅           | ✅       | ✅     |
| Publish apps    | ❌      | ❌           | ✅       | ✅     |
| Manage users    | ❌      | ❌           | Limited | ✅     |

---

# Most Important Rule

Contributor:

Can publish content.

Cannot publish apps.

---

Member:

Can publish apps.

---

Admin:

Controls workspace.

---

# A.13 Endorsement Comparison

| Type      | Meaning             |
| --------- | ------------------- |
| Promoted  | Recommended         |
| Certified | Officially approved |

---

# Certified requires:

* Authorized approval
* Organizational process

---

# A.14 Refresh Decision Guide

| Requirement            | Solution          |
| ---------------------- | ----------------- |
| Update imported data   | Refresh           |
| Automate updates       | Scheduled refresh |
| Local database refresh | Gateway           |
| Real-time data         | DirectQuery       |

---

# Appendix A Final Reminder

The PL-300 rewards knowing:

**Which Power BI feature solves the business requirement.**

Do not memorize definitions only.

Think:

Requirement → Feature → Reason