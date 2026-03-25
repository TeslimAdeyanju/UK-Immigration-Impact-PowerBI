# UK Immigration Impact Analysis — Power BI Portfolio Project

> **Status: In Progress** — Model is being built incrementally. See milestones below for current progress.

---

## Project Overview

This project analyses the impact of immigration on the United Kingdom using official Home Office and ONS datasets (2025 release). It is built as a portfolio Power BI project using the modern **PBIP format** with **TMDL (Tabular Model Definition Language)** — enabling full version control of the semantic model.

The report covers the full immigration lifecycle: visa applications and outcomes, asylum claims, detention, returns, settlement, and citizenship — cross-referenced with economy data including employment, earnings, and local skills demand.

---

## Data Sources

All data is sourced from official UK government datasets.

### Home Office — Immigration & Asylum (Sep 2025 release)

| File | Dataset | Coverage |
|---|---|---|
| `1-entry-clearance-visa-outcomes-datasets-sep-2025.xlsx` | Visa applications & outcomes by nationality and visa type | 2005–2025 Q2 |
| `2-asylum-claims-datasets-sep-2025.xlsx` | Asylum claims raised + route of entry | 2001–2025 Q3 |
| `3-asylum-seekers-receipt-support-datasets-sep-2025.xlsx` | Asylum seekers in receipt of Home Office support | 2014–2025 Q3 |
| `4-support-local-authority-datasets-sep-2025.xlsx` | Asylum support by Local Authority | 2014–2025 Q3 |
| `5-detention-datasets-sep-2025.xlsx` | Immigration detention | 2010–2025 Q3 |
| `6-returns-datasets-sep-2025.xlsx` | Returns (voluntary + enforced) | 2010–2025 Q3 |
| `7-settlement-datasets-sep-2025.xlsx` | Settlement grants and refusals | 2007–2025 Q3 |
| `8-citizenship-datasets-sep-2025.xlsx` | British citizenship applications | 2004–2025 Q3 |

### ONS — Economy Data

| File | Content |
|---|---|
| `1-mye24tablesuk.xlsx` | Mid-Year Population Estimates by Local Authority |
| `3-emp06nov2025.xls` | Employment statistics |
| `4-earn06nov2025.xls` | Earnings / wages statistics |
| `5-LocalSkillsDataset.xlsx` | Local skills demand by region and sector |
| `6-dt051-table-11.csv` | Housing / deprivation index |

---

## Tech Stack

| Tool | Usage |
|---|---|
| **Power BI Desktop** | Report and model authoring |
| **PBIP + TMDL format** | Version-controlled semantic model (text-based) |
| **Power Query (M)** | Data transformation |
| **DAX** | Measures and calculated columns |
| **GitHub** | Version control and portfolio hosting |
| **Claude Code** | AI-assisted model development |

---

## Project Milestones

### Milestone 1 — Project Setup & Version Control
- [x] Organise raw data files into `asylum_data/` and `economy_data/` folders
- [x] Create Power BI project in PBIP format (TMDL enabled)
- [x] Initialise Git repository
- [x] Push to GitHub with clean history (no secrets)
- [x] Set up `.gitignore` for Power BI temp files

### Milestone 2 — Establish Naming Conventions
- [ ] Define and document table naming standards
  - `Fact *` — transactional fact tables
  - `Dim *` — dimension / lookup tables
  - `Supp *` — supplementary aggregated tables
  - `_Measures` — DAX measures table (disconnected)
- [ ] Column naming: Title Case, spaces not underscores

### Milestone 3 — Rename & Clean Existing Tables *(in progress)*
- [x] Rename staging expressions to proper Fact table names
- [x] Rename dimension lookup tables (`Dim Nationality`, `Dim Visa Type`)
- [x] Delete duplicate `Fact Visa Applications (2)` table
- [x] Update all cross-references (relationships, model, diagram layout)

### Milestone 4 — Transform Partially-Built Tables
- [ ] `Supp Asylum Support Recipients` — unpivot period columns, rename columns
- [ ] `Supp Asylum Support by Local Authority` — unpivot, rename
- [ ] `Supp Detention Population` — unpivot, rename
- [ ] `Supp Returns by Nationality` — unpivot, rename
- [ ] `Supp Returns by Destination` — unpivot, rename
- [ ] `Supp Settlement Decisions` — unpivot, rename
- [ ] `Supp Settlement Grants by Demographics` — unpivot, rename
- [ ] `Supp Citizenship Applications` — unpivot, rename

### Milestone 5 — Transform Raw Tables
- [ ] `Supp Asylum Outcomes by Type` — promote headers, rename, type columns
- [ ] `Supp Detention Entries` — promote headers, rename, type columns
- [ ] `Supp Detention by Centre` — promote headers, rename, type columns
- [ ] `Supp Returns by Nationality Detail` — promote headers, rename, type columns
- [ ] `Supp Returns by Type` — promote headers, rename, type columns
- [ ] `Supp Settlement by Nationality` — promote headers, rename, type columns
- [ ] `Supp Citizenship Grants by Nationality` — promote headers, rename, type columns

### Milestone 6 — Build Star Schema Dimensions
- [ ] `Dim Period` — quarterly period table with `Period Key` for relationships
- [ ] `Dim Applicant Type` — extracted from fact tables
- [ ] `Dim Sex` — from asylum claims data
- [ ] `Dim Age Group` — from asylum claims data with age band groupings
- [ ] Expand `Dim Nationality` — add World Region Group, EU/EEA flag
- [ ] Expand `Dim Visa Type` — add Visa Category (Work / Study / Family / Humanitarian / Other)

### Milestone 7 — Build Relationships
- [ ] Connect all Fact tables to `Dim Period`, `Dim Nationality`, `Dim Visa Type`
- [ ] Connect `Fact Asylum Claims` to `Dim Sex`, `Dim Age Group`
- [ ] Connect all Supp tables to `Dim Period`
- [ ] Validate cardinality and filter direction on all relationships

### Milestone 8 — DAX Measures
- [ ] Volume measures (Applications, Claims, Returns, Detained, etc.)
- [ ] Rate measures (Visa Grant Rate, Refusal Rate, Asylum Recognition Rate)
- [ ] Period comparison measures (YoY %, Quarter-over-Quarter)
- [ ] Share / composition measures (% by nationality, % by visa type)
- [ ] Ranking measures (Top 10 nationalities, cumulative totals)

### Milestone 9 — Economy Data Integration
- [ ] Load population data → per-capita KPIs
- [ ] Load employment data → immigration vs. employment rate analysis
- [ ] Load earnings data → immigration vs. wages analysis
- [ ] Load skills data → visa types mapped to regional skill gaps
- [ ] Economy DAX measures (Asylum Seekers per 10,000 Population, etc.)

### Milestone 10 — Report Design & Publication
- [ ] Design report pages for each analytical theme
- [ ] Apply consistent theme and formatting
- [ ] Add tooltips, bookmarks, and navigation
- [ ] Publish to Power BI Service
- [ ] Document insights and key findings

---

## Repository Structure

```
📁 asylum_data/          → Home Office immigration datasets (Excel/CSV)
📁 economy_data/         → ONS economy datasets (Excel/CSV)
📁 Immigration_analysis_2025.SemanticModel/
│   📁 definition/
│   │   📁 tables/       → One .tmdl file per table (version-controlled schema)
│   │   expressions.tmdl → Power Query (M) staging queries
│   │   model.tmdl       → Model-level settings and query groups
│   │   relationships.tmdl → All model relationships
│   └── diagramLayout.json
📁 Immigration_analysis_2025.Report/
│   📁 definition/       → Report pages and visuals (JSON)
Immigration_analysis_2025.pbip  → Power BI Project entry point
```

---

## Author

**Teslim Adeyanju** — Data Analyst Portfolio Project, 2025

---

*Data sourced from UK Home Office and ONS open data. All datasets are publicly available under the Open Government Licence.*
