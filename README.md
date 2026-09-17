# 📊 Route Prioritization & Digital Adoption System
### (Portfolio Project — Anonymized Data)

## 📌 Executive Summary

Data-driven analytical system designed to prioritize 22 commercial routes based on their digital adoption potential for a B2B ordering application.

**Key Outcome:** The Top 10 routes concentrate 48.9% of the total adoption potential. Additionally, 38.4% of registered clients remain inactive on the app, presenting an immediate quick-win opportunity.

---

## 🔒 Note on Data & Confidentiality

This project is based on an end-to-end commercial analysis originally developed for a Consumer Packaged Goods (CPG) company, whose original data is confidential. For portfolio purposes:

- The company is presented under the synthetic name **"Bebidas del Norte S.A."**
- Client IDs, store names, route codes, and geographic hierarchies (region, division, district, distribution center) are **100% synthetic**.
- **Statistical distributions and scoring logic remain identical to the original project**: total client count (1,788), Top 10 potential concentration (48.9%), score range (22.40–47.50), and global category distribution (25.6% / 38.4% / 22.4% / 13.6%).
- Line-by-line verification confirmed that no real client, route code, or proprietary identifier appears in this version.

---

## 🎯 Business Problem

Where should commercial and field operations allocate resources to maximize B2B digital adoption across ~1,788 clients at different onboarding stages?

---

## 🛠️ Tech Stack

- **Python (Pandas):** ETL pipeline, data cleaning, and dataset transformation.
- **SQL (SQLite):** Multi-table join integration, CTEs, and route-level aggregation.
- **Looker Studio / Power BI:** Executive interactive dashboards, route heatmaps, and funnel visualizations.
- **Jupyter Notebooks:** Exploratory Data Analysis (EDA), cohort modeling, and documentation.

---

## 📐 Methodology

### 1. Client Segmentation Criteria

| Category | Definition / Rule |
| :--- | :--- |
| **Non-Registered** | No active account in the mobile app |
| **Registered Non-Digital** | Account created, 0% digital purchases |
| **Hybrid** | 1% – 69% digital purchase share |
| **Fully Digital** | ≥ 70% digital purchase share |

---

### 2. Weighted Priority Scoring Model

**Formula:**
$$\text{Score} = (\% \text{Reg. Non-Digital} \times 0.40) + (\% \text{Non-Reg.} \times 0.25) + (\% \text{Hybrids} \times 0.20) + ((100 - \% \text{Fully}) \times 0.15)$$

**Weights Justification:**
- **40% Registered Non-Digital:** High-priority quick wins (clients already onboarded, requiring activation only).
- **25% Non-Registered:** Acquisition volume (requires account registration + activation).
- **20% Hybrids:** Scalable accounts (already familiar with the B2B platform).
- **15% Fully Digital Gap:** Contextual growth margin.

**Score Scale:** 0 to 60 points (*higher score = higher digitalization priority*).

---

### 3. ETL & Data Pipeline

- SQLite database (`digital_adoption.db`) linking transaction and registration tables via CTEs and `LEFT JOIN` operations.
- Aggregation by commercial route with calculated percentage distributions per category.
- Automated priority score calculation directly within the SQL query pipeline.

---

### 4. Interactive Dashboard & Bottleneck Funnel Analysis

- **Page 1 — Route Prioritization View:** High-level KPIs, priority heatmap table, Top routes ranking, global adoption status distribution, and gauge indicators.
- **Page 2 — Client Universe & Funnel Analysis:**
  - **Funnel Visualizer:** Displays the conversion funnel across all 4 digital adoption stages (*Non-Registered ➔ Registered Non-Digital ➔ Hybrid ➔ Fully Digital*).
  - **Route-Level Bottleneck Identification:** Filtering by a specific route dynamically updates the funnel chart, exposing the exact drop-off stage (e.g., routes blocked at initial registration vs. routes stuck at hybrid adoption).
---

##  Key Business Findings

1. **38.4% of registered clients do not use the app** → Immediate quick-win target for field representatives.
2. **Top 10 routes concentrate 48.9% of total digital potential** → Focus resource deployment on these high-impact territories.
3. **Route Priority Scores range from 22.40 (highly digitalized) to 47.50 (urgent priority)**.
4. **Global Adoption Distribution:** 25.6% Non-Registered, 38.4% Registered Non-Digital, 22.4% Hybrid, and 13.6% Fully Digital.

---

##  Repository Structure


Proyecto_Adopcion_Digital_Portafolio/
│
├── Data_raw_anon/               # Raw synthetic datasets (CSV)
├── Data_processed_anon/        # Processed CSVs + SQLite DB (digital_adoption.db)
├── Notebooks/
│   ├── 01_Exploración y limpieza de datos full digital.ipynb
│   ├── 02_Exploración y limpieza de datos registros de clientes.ipynb
│   ├── 03_Transformación de datos.ipynb
│   └── 04_digital_adoption_cohort_analysis.ipynb
├── Reportes_anon/
│   └── Informe_Adopcion_Digital_Anonimizado.pdf
└── README.md

---
## Author

Felipe de Jesús Luis Rios

Data & Program Operations Analyst

📧 felipedejesusluisrios@gmail.com |