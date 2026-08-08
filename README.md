# HR Attrition Analytics Dashboard

**An end-to-end People Analytics engagement: diagnosing why employees leave, quantifying the cost, and directing retention investment to where it will move the needle, built on Microsoft Fabric and Power BI.**

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![Microsoft Fabric](https://img.shields.io/badge/Microsoft_Fabric-0078D4?style=flat&logo=microsoftazure&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-742774?style=flat)
![License](https://img.shields.io/badge/License-MIT-green.svg)

📊 **[View Live Dashboard](https://app.fabric.microsoft.com/links/beNxlPJ9tw?ctid=e93d71d6-b5c0-4b78-a861-d9964ecdfcd6&pbi_source=linkShare)** &nbsp;|&nbsp; 📄 [Business Requirements Document](Docs/BRD_HR_Attrition_Dashboard.docx) &nbsp;|&nbsp; 📽️ [Stakeholder Presentation](Docs/HR_Attrition_Presentation.pptx)

---

## Table of Contents
- [Executive Summary](#executive-summary)
- [Live Dashboard](#live-dashboard)
- [Business Problem](#business-problem)
- [Project Deliverables](#project-deliverables)
- [Dataset Description](#dataset-description)
- [Tools & Technologies](#tools--technologies)
- [Project Structure](#project-structure)
- [Methodology](#methodology)
- [Key Findings](#key-findings)
- [Dashboard Walkthrough](#dashboard-walkthrough)
- [Governance & Data Security](#governance--data-security)
- [How to Run This Project](#how-to-run-this-project)
- [Recommendations & Roadmap](#recommendations--roadmap)
- [Author & Contact](#author--contact)

---

## Executive Summary

This project was scoped and delivered the way a People Analytics function inside a large enterprise or advisory practice would run it: starting with a **signed-off Business Requirements Document**, not a spreadsheet. Every downstream artifact, the data model, the dashboard, the executive readout, traces back to the business questions defined up front.

The result: HR Leadership can now answer in **seconds**, self-service, questions that previously took days of manual data pulls, and can point retention spend at the segments where it will actually reduce cost, backed by evidence rather than anecdote.

| | |
|---|---|
| **Overall attrition rate** | **16.1%** (vs. 10 to 15% industry benchmark) |
| **Headcount analyzed** | 1,470 employees |
| **Highest-risk segment** | Sales Representatives, 39.8% attrition |
| **Time-to-insight** | Days to seconds, self-service dashboard |

## Live Dashboard

📊 **[Open the interactive Power BI dashboard](https://app.fabric.microsoft.com/links/beNxlPJ9tw?ctid=e93d71d6-b5c0-4b78-a861-d9964ecdfcd6&pbi_source=linkShare)**

Explore the report live in your browser, no download required. Requires access via the linked Microsoft Fabric/Power BI workspace.

## Business Problem

HR Leadership needed to understand why employees were leaving the organization and where to focus retention efforts. Losing trained personnel drives significant hiring, onboarding, and salary-replacement costs, making attrition reduction a top corporate priority, yet no centralized, governed source of truth existed to act on.

Before any data work began, the engagement was scoped through a formal **[Business Requirements Document](Docs/BRD_HR_Attrition_Dashboard.docx)**, defining objectives, in/out-of-scope boundaries, stakeholders, and success metrics. This is the standard a management-consulting or enterprise analytics team holds itself to before touching a dataset.

The dashboard was built to answer three core business questions:

1. **What is the overall attrition rate?**
2. **Which departments are losing the most employees?**
3. **What is the relationship between pay, age, and an employee's decision to leave?**

## Project Deliverables

This repository is structured as a complete analytics engagement, not just a dashboard file.

| Deliverable | Purpose |
|---|---|
| **[Business Requirements Document](Docs/BRD_HR_Attrition_Dashboard.docx)** | Problem definition, scope, stakeholders, and success criteria, agreed before build |
| **[HR Attrition Analysis.pbix](Dashboard/HR%20Attrition%20Analysis.pbix)** | Full interactive Power BI report |
| **[HR Attrition Analysis.pbit](Dashboard/HR%20Attrition%20Analysis.pbit)** | Reusable template for rebuilding against new data |
| **[Stakeholder Presentation](Docs/HR_Attrition_Presentation.pptx)** | Executive-ready summary of problem, method, and findings |
| **[Live Dashboard link](https://app.fabric.microsoft.com/links/beNxlPJ9tw?ctid=e93d71d6-b5c0-4b78-a861-d9964ecdfcd6&pbi_source=linkShare)** | Published, governed report for HR Leadership self-service |

## Dataset Description

| Detail | Description |
|---|---|
| **File** | `HR-Employee-Attrition.csv` |
| **Records** | 1,470 employees |
| **Grain** | One row per employee |
| **Source** | [IBM HR Analytics Employee Attrition Dataset](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset) |
| **Key Fields** | `Age`, `Attrition`, `Department`, `JobRole`, `MonthlyIncome`, `OverTime`, `BusinessTravel`, `MaritalStatus`, `Gender`, `EducationField`, `YearsAtCompany` |
| **Engineered Fields** | `Salary Band` (income bracket), `Age Group` (age bracket), created in Dataflow Gen2 to simplify visual analysis |

## Tools & Technologies

| Category | Tool |
|---|---|
| Requirements & Scoping | Business Requirements Document (Word) |
| Data Ingestion & ETL | Microsoft Fabric, Dataflow Gen2 |
| Data Storage | Microsoft Fabric, Lakehouse (OneLake) |
| Semantic Modeling | Power BI Semantic Model, DAX |
| Visualization | Power BI Desktop / Power BI Service |
| Governance | Column-Level Security (Fabric OneLake Security) |
| Stakeholder Communication | PowerPoint executive readout |
| Version Control | Git & GitHub |

## Project Structure

```
hr-attrition-insights/
├── Dashboard/
│   ├── HR Attrition Analysis.pbix       # Full Power BI report
│   ├── HR Attrition Analysis.pbit       # Reusable template version
│   └── Readme
├── Data/
│   ├── HR-Employee-Attrition.csv        # Raw source dataset
│   └── Readme
├── Docs/
│   ├── BRD_HR_Attrition_Dashboard.docx  # Business Requirements Document
│   ├── HR_Attrition_Presentation.pptx   # Executive stakeholder deck
│   └── Readme
├── Screenshots/
│   ├── Fabric.png                       # Fabric workspace setup
│   ├── Lakehouse.png                    # Lakehouse table load
│   ├── Schematic model.png              # Semantic model view
│   ├── Overview.png                     # Dashboard, Overview page
│   ├── Deep Dive.png                    # Dashboard, Deep Dive page
│   └── Readme
├── LICENSE
└── README.md
```

## Methodology

**1. Requirements first.** Objectives, scope, and success metrics were documented and agreed in the BRD before any pipeline work began, preventing scope creep and keeping the build accountable to the business questions it exists to answer.

**2. Data Cleaning & Preparation.** Performed inside **Dataflow Gen2** prior to loading into the Lakehouse:
- Connected to the raw CSV via the Web/CSV connector (Anonymous auth, UTF-8 encoding, comma-delimited); data types auto-evaluated from the first 200 rows.
- Created a **Salary Band** calculated column, grouping `MonthlyIncome` into readable brackets (`Under 3K`, `3K to 6K`, `6K to 10K`, etc.) to reduce visual clutter and unlock grouped analysis.
- Created an **Age Group** calculated column, banding raw ages (`18 to 25`, `25 to 35`, `35 to 45`, `Above 45`), keeping categories to 5 to 7 groups for clean visuals.
- Explicitly set data types on both engineered columns before loading, required for a successful Lakehouse import.
- Loaded the cleaned flat table into the Fabric Lakehouse and built a semantic model directly on top of it. A flat-table design was chosen over a star schema, since the dataset is under 2,000 rows.

**3. Semantic Modeling.** Five core DAX measures power the dashboard, **Attrition Rate**, **Head Count**, **Employees Left**, **Average Monthly Income**, and **Average Tenure of Leavers**, deliberately built as measures rather than raw column drags, to keep KPI logic centralized and auditable.

## Key Findings

- 📉 **Overall attrition rate: 16.1%**, above the 10 to 15% industry average, signaling a real organizational risk.
- 🏢 **Sales** has the highest departmental attrition (20.6%), followed by HR (19.0%) and R&D (13.8%).
- 💼 **Sales Representatives** are the highest-risk job role at **39.8% attrition**, more than double the org average.
- 💰 **Lower salary bands correlate strongly with attrition.** The "Under 3K" band skews heavily toward departures.
- 🎂 **Younger employees (18 to 25) leave at nearly 4x the rate** of employees aged 45 to 60 (35.8% vs. 12.5%).
- ⏰ **Overtime workers leave far more often** than those who don't, one of the strongest single predictors of attrition.
- ✈️ **Frequent business travelers** show almost 3x the attrition rate of non-travelers (24.9% vs. 8.0%).
- 💍 **Single employees** leave at more than double the rate of married employees (25.5% vs. 12.5%).
- 👥 **Gender split reverses by department.** Men leave more company-wide (17.0% vs. 14.8%), but women leave more within HR specifically, a nuance only visible through drill-down.

## Dashboard Walkthrough

📊 **[View Live Dashboard](https://app.fabric.microsoft.com/links/beNxlPJ9tw?ctid=e93d71d6-b5c0-4b78-a861-d9964ecdfcd6&pbi_source=linkShare)**

The report is built as a **two-page, cross-filterable Power BI experience** with a custom color theme (Red = negative, Green = positive, Yellow = neutral), drop-down slicers (Department, Gender, Salary Band), a hover-activated **Clear All Slicers** reset button, and a **Page Navigator** for smooth, web-style switching.

### Overview Page
KPI cards, attrition tree map, attrition-by-department bar chart, decomposition tree (Department → Job Role → Salary Band), and a job-role matrix with conditional data bars.

![Overview Page](Screenshots/Overview.png)

### Deep Dive Page
Age Group risk matrix with conditional color bands (green/yellow/red), and operational driver breakdowns for OverTime, Business Travel, Marital Status, and Gender.

![Deep Dive Page](Screenshots/Deep%20Dive.png)

## Governance & Data Security

`MonthlyIncome` is restricted at the default reader role via Fabric's **OneLake Column-Level Security**, so general viewers can explore attrition patterns without ever seeing individual salary values, while authorized workspace roles retain full access. This mirrors how compensation data is handled in a real enterprise HR analytics environment, where insight and confidentiality have to coexist.

## How to Run This Project

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/hr-attrition-insights.git
   ```
2. **Review the requirements.** Read [`Docs/BRD_HR_Attrition_Dashboard.docx`](Docs/BRD_HR_Attrition_Dashboard.docx) for the full problem scope and success criteria.
3. **Open the report.**
   - View it live via the **[Live Dashboard link](https://app.fabric.microsoft.com/links/beNxlPJ9tw?ctid=e93d71d6-b5c0-4b78-a861-d9964ecdfcd6&pbi_source=linkShare)**, or
   - Open `Dashboard/HR Attrition Analysis.pbix` in **Power BI Desktop** to explore the full report, or
   - Open the `.pbit` template and point it at your own copy of `Data/HR-Employee-Attrition.csv` to rebuild from scratch.
4. **(Optional) Rebuild the Fabric pipeline.**
   - Create a Fabric workspace, add a Dataflow Gen2, connect it to `Data/HR-Employee-Attrition.csv`, and recreate the Salary Band / Age Group transformation steps described above.
   - Load into a Lakehouse and build a semantic model on the flat table.
5. **Explore** using the Department, Gender, and Salary Band slicers, and drill into the Decomposition Tree for root-cause paths.
6. **Present it.** [`Docs/HR_Attrition_Presentation.pptx`](Docs/HR_Attrition_Presentation.pptx) is ready to walk a stakeholder audience through the same story end to end.

## Recommendations & Roadmap

**Recommendations:**
- Prioritize retention budget on **Sales / Sales Representatives** and the **Under 3K salary band**, the two segments with the highest concentration of departures.
- Review overtime policy and workload distribution, given its strong association with attrition.
- Investigate travel-heavy roles for burnout risk and consider hybrid travel policies for frequent travelers.
- Design targeted onboarding/engagement programs for employees under 25, the highest-attrition age group.

**Roadmap:**
- Add a predictive attrition-risk model (Machine Learning) to score active employees.
- Integrate Fabric Data Activator for automated alerts when a department's attrition rate crosses a threshold.
- Introduce periodic snapshots or an exit-date field to enable true time-series trend analysis.
- Enable Fabric Copilot for natural-language Q&A over the semantic model.

## Author & Contact

**Seema Kumari**
Data Analyst | Business Intelligence & Microsoft Fabric

- 📧 Email: [seemakri136@gmail.com](mailto:seemakri136@gmail.com)
- 💼 LinkedIn: [linkedin.com/in/seema-kumari-375763308](https://linkedin.com/in/seema-kumari-375763308)

---

⭐ If you found this project useful, consider giving it a star. It helps others discover it.
