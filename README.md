# Actual vs Target Sales KPI Variance Dashboard (Power BI)

[![Power BI](https://img.shields.io/badge/Platform-Power%20BI%20Desktop-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](#)
[![DAX](https://img.shields.io/badge/Formulas-Advanced%20DAX-orange?style=for-the-badge)](#)
[![Data Modeling](https://img.shields.io/badge/Modeling-Dual--Fact%20Star%20Schema-blue?style=for-the-badge)](#)

---

## 📌 Project Overview
An executive-level corporate finance and sales performance dashboard built in Microsoft Power BI. The report monitors \$19M+ in gross revenue across 14 months (January 2023 – February 2024), tracking actual sales performance against budgeted targets across multiple sales teams and representatives.

Designed with an executive layout, custom corporate branding, and dynamic DAX indicators to quickly spot underperforming teams, revenue leakages, and budget variances.

---

## 🏗️ Data Architecture & Modeling
Raw records originally structured as cross-tabulated matrix spreadsheets were ingested and normalized using **Power Query**:
* **Data Transformation:** Unpivoted historical monthly performance matrices for both Actuals and Targets into long-format relational tables.
* **Dual-Fact Architecture:** Implemented a multi-fact star schema connecting two central fact tables (`Fact_Actuals` and `Fact_Targets`) with shared dimension tables:
  * `Dim_Calendar` (Date & monthly intervals)
  * `Dim_People` (Sales team hierarchy, employee names, and profile avatars)

---

## 📈 Key KPIs & Analytical Measures

### 1. Revenue & Budget Variance
* **Total Sales Actual:** `SUM(Fact_Actuals[Sales])`
* **Total Sales Target:** `SUM(Fact_Targets[Sales])`
* **Variance (\$):** `[Total Sales Actual] - [Total Sales Target]`
* **Variance (%):** `DIVIDE([Variance], [Total Sales Target], 0)`

### 2. Time Intelligence (YTD)
* **YTD Actuals & Targets:** Formulated using `DATESYTD` to track running cumulative performance across the fiscal cycle.

### 3. Dynamic Thresholds & Visual DAX
* **Win/Loss Status:** Evaluates whether target was achieved (`IF([Variance] > 0, 1, -1)`) to drive dynamic visual status indicators.
* **Dynamic Status Indicators:** DAX-generated strings integrating visual icons (`🟢 / 🔴`) directly into chart labels based on positive or negative variance.
* **Context-Aware Dynamic Titles:** Automated chart header logic (e.g., *"Targets met for X out of 14 months"*) that recalculates dynamically as slicers are filtered.

---

## 🖥️ Dashboard Visuals & Features

* **Executive KPI Cards:** New Multi-row card visual displaying high-level Actuals, Targets, Variance, and Year-to-Date (YTD) reference benchmarks.
* **Overlapping Actual vs. Target Columns:** Dual-layer column chart highlighting actual revenue delivery against transparent target benchmark bars.
* **Win-Loss Distribution:** Color-coded monthly timeline marking target achievement months vs. deficit months.
* **Sales Team Drilldown Matrix:** Granular operational table featuring employee avatars, actual vs. target delivery, conditional formatting data bars, and embedded mini sparklines.
* **Interactive Slicers:** Dynamic team and period filtering with instant cross-visual highlighting.
