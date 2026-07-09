# Chapter 6 — Visualizations, Reports, and Data Analysis Features

## Microsoft Power BI Data Analyst Associate (PL-300)

---

# Chapter Objectives

After completing this chapter, learners should understand:

* Choosing appropriate visuals
* Configuring report pages
* Using slicers and filters
* Drill down vs drillthrough
* Tooltips
* Bookmarks
* Sync slicers
* Conditional formatting
* AI visuals
* Report accessibility
* Common PL-300 visualization scenarios

---

# 6.1 Purpose of Data Visualization

A good visualization communicates insights clearly.

A report should help users answer:

* What happened?
* Why did it happen?
* What should we do?

---

# Visualization Selection

Choose visuals based on the business question.

---

# 6.2 Common Visual Types

---

# Bar / Column Charts

Best for:

Comparing categories.

Example:

Sales by Product Category

---

Use when asking:

> Which category performed best?

---

# Line Charts

Best for:

Trends over time.

Example:

Monthly Revenue

---

Use when asking:

> How is something changing?

---

# Pie / Donut Charts

Best for:

Simple part-to-whole comparisons.

Example:

Market Share

---

PL-300 Note:

Avoid when there are many categories.

---

# Scatter Charts

Used for:

Relationships between two numerical values.

Example:

Sales vs Profit

---

# Maps

Used for:

Geographic analysis.

Example:

Sales by State

---

# Cards

Used for:

Single important values.

Examples:

* Total Revenue
* Customer Count
* Profit Margin

---

# Tables and Matrices

Used for:

Detailed values.

Matrix supports:

* Hierarchies
* Drill down

---

# 6.3 Slicers

A slicer is a visual filter.

Example:

Region slicer:

* East
* West
* North

Selecting:

East

filters visuals.

---

# Slicer Uses

Good for:

* User-driven filtering
* Interactive reports

---

# Common Slicer Types

* List
* Dropdown
* Between
* Before/After
* Relative date

---

# PL-300 Scenario

A user wants report consumers to choose a sales region.

Use:

✅ Slicer

---

# 6.4 Filters

Filters restrict data displayed in visuals.

Power BI has three major filter levels.

---

# Visual Level Filter

Affects one visual.

Example:

Only show products with sales > $10,000.

---

# Page Level Filter

Affects all visuals on one page.

Example:

Only show 2026 sales.

---

# Report Level Filter

Affects every page.

Example:

Only show North America data.

---

# Filters vs Slicers

| Filters               | Slicers         |
| --------------------- | --------------- |
| Designer controlled   | User controlled |
| Hidden by default     | Visible visual  |
| Applied through panes | Interactive     |

---

# 6.5 Drill Down

Drill down explores levels within the same visual.

Example:

Date hierarchy:

```id="g0kl4m"
Year

↓

Quarter

↓

Month

↓

Day
```

User clicks:

2026

↓

January

---

# Drill Down Requires:

A hierarchy.

---

# Drill Up

Returns to higher level.

Example:

Month → Year

---

# 6.6 Drillthrough

Drillthrough navigates to another report page.

Example:

Sales Summary Page:

Click:

Product A

↓

Product Detail Page

Showing:

* Customers
* Orders
* Profit

---

# Drill Down vs Drillthrough

| Drill Down         | Drillthrough                |
| ------------------ | --------------------------- |
| Same visual        | Different page              |
| Requires hierarchy | Requires drillthrough field |
| More detail        | Detailed analysis           |

---

# PL-300 Trap

Drill down and drillthrough are the same.

❌ Incorrect

They solve different problems.

---

# 6.7 Tooltips

Tooltips show additional information when hovering.

Example:

Hover over sales bar:

Shows:

* Profit
* Margin
* Customer count

---

# Report Page Tooltips

A tooltip can be a custom report page.

Benefits:

* More detail
* Additional visuals
* Better storytelling

---

# Tooltip vs Drillthrough

Tooltip:

Hover

Drillthrough:

Navigate

---

# 6.8 Bookmarks

Bookmarks save the current state of a report.

They can capture:

* Filters
* Slicers
* Visibility
* Page location

---

# Bookmark Uses

Common examples:

## Navigation

Create buttons to move between pages.

---

## Show/Hide Objects

Example:

Button toggles a filter panel.

---

## Presentation Mode

Create guided reports.

---

# PL-300 Scenario

A report has a button that hides and shows a filter panel.

Use:

✅ Bookmark

---

# 6.9 Sync Slicers

Sync slicers allow one slicer to control multiple pages.

Example:

Region slicer:

Page 1:

Sales Overview

Page 2:

Profit Analysis

Both respond.

---

# PL-300 Scenario

A user wants the same year slicer available across several pages.

Use:

✅ Sync slicers

---

# 6.10 Conditional Formatting

Conditional formatting changes appearance based on values.

Examples:

* Data bars
* Icons
* Color scales

---

Example:

Profit:

Positive:

Green indicator

Negative:

Red indicator

---

# Used For:

* Highlighting trends
* Identifying exceptions

---

# 6.11 AI Visuals

Power BI includes AI-assisted visuals.

---

# Key Influencers

Purpose:

Find factors that influence a metric.

Example:

Question:

"What influences customer satisfaction?"

Possible answers:

* Product category
* Region
* Customer type

---

# Decomposition Tree

Purpose:

Explore a measure by dimensions.

Example:

Why did sales decrease?

Analyze by:

1. Region
2. Product
3. Salesperson

---

# Key Influencers vs Decomposition Tree

| Key Influencers      | Decomposition Tree        |
| -------------------- | ------------------------- |
| Finds factors        | Explores breakdown        |
| Explains drivers     | Interactive investigation |
| Statistical analysis | User exploration          |

---

# Q&A Visual

Allows users to ask questions using natural language.

Example:

"What were sales last year?"

---

# Smart Narrative

Automatically generates text summaries.

---

# 6.12 Accessibility

PL-300 expects awareness of accessible reports.

Best practices:

* Use meaningful titles
* Avoid relying only on colors
* Provide alt text
* Use sufficient contrast
* Organize reading order

---

# 6.13 Report Design Best Practices

Good reports:

* Have clear purpose
* Avoid unnecessary visuals
* Highlight important metrics
* Use consistent formatting
* Provide context

---

# Avoid:

* Too many visuals
* Excessive colors
* Cluttered pages

---

# 6.14 Common PL-300 Exam Traps

---

## Trap 1

Use a pie chart for hundreds of categories.

❌ Incorrect

Pie charts work best with few categories.

---

## Trap 2

Drillthrough expands levels in the same chart.

❌ Incorrect

That is drill down.

---

## Trap 3

Bookmarks only save page navigation.

❌ Incorrect

They save report state.

---

## Trap 4

Tooltips navigate to another page.

❌ Incorrect

Drillthrough navigates.

---

## Trap 5

Slicers and filters are identical.

❌ Incorrect

Slicers are visible interactive filters.

---

## Trap 6

Key Influencers and Decomposition Tree do the same thing.

❌ Incorrect

Key Influencers finds drivers.

Decomposition Tree explores breakdowns.

---

# Chapter 6 Practice Questions

---

# Question 1

A user wants to analyze monthly revenue trends.

Which visual should be used?

A. Pie chart

B. Line chart

C. Card

D. Table

Correct Answer:

✅ B. Line chart

---

# Question 2

A user wants to select a region and filter all visuals on a page.

What should be used?

A. Bookmark

B. Slicer

C. Tooltip

D. Drillthrough

Correct Answer:

✅ B. Slicer

---

# Question 3

A user wants to move from a summary page to a detailed customer page.

What feature should be used?

A. Drill down

B. Drillthrough

C. Tooltip

D. Conditional formatting

Correct Answer:

✅ B. Drillthrough

---

# Question 4

A user wants the same date slicer available across multiple report pages.

What should be configured?

A. Bookmarks

B. Sync slicers

C. Tooltips

D. Filters

Correct Answer:

✅ B. Sync slicers

---

# Question 5

A manager asks:

"What factors influence customer churn?"

Which visual should be used?

A. Key Influencers

B. Card

C. Matrix

D. Gauge

Correct Answer:

✅ A. Key Influencers

---

# Question 6

An analyst wants to investigate why revenue decreased by breaking it down by dimensions.

Which visual should be used?

A. Decomposition Tree

B. Pie chart

C. Line chart

D. Slicer

Correct Answer:

✅ A. Decomposition Tree

---

# Chapter 6 Summary

| Concept                | Purpose                |
| ---------------------- | ---------------------- |
| Column Chart           | Compare categories     |
| Line Chart             | Show trends            |
| Card                   | Display KPIs           |
| Slicer                 | User filtering         |
| Filters                | Restrict data          |
| Drill Down             | Explore hierarchy      |
| Drillthrough           | Navigate to details    |
| Tooltip                | Show extra information |
| Bookmark               | Save report state      |
| Sync Slicer            | Control multiple pages |
| Conditional Formatting | Highlight values       |
| Key Influencers        | Find drivers           |
| Decomposition Tree     | Explore causes         |

---

# Next Chapter

## Chapter 7 — Advanced Power BI Features and Analytics

Topics:

* Advanced visuals
* AI capabilities
* Q&A
* Smart Narrative
* What-if parameters
* Analyze in Excel
* Export options
* Performance Analyzer
* Optimization techniques
* PL-300 advanced scenarios
