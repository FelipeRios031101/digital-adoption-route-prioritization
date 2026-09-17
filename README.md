#  Route Prioritization & Digital Adoption Dashboard
### (Portfolio Project — Anonymized Data)

##  Executive Summary

An end-to-end commercial analytics system designed to prioritize 22 commercial routes (`ruta_sap`) across 1,789 clients based on their B2B digital adoption potential.

**Key Outcome:** Identifies high-priority routes using a custom weighted scoring model (Scores ranging from 22.4 to 47.5, with an average score of 39.1). The system highlights immediate opportunities, such as high proportions of registered non-digital clients, allowing field teams to optimize commercial routing.

---

##  Note on Data & Confidentiality

This project is based on an end-to-end commercial analysis originally developed for a Consumer Packaged Goods (CPG) company, whose original data is confidential. For portfolio purposes:

- The company is presented under the synthetic name **"Bebidas del Norte S.A."**
- Client IDs (`cliente_id`), store names (`nombre_cliente`), route codes (`ruta_sap`), and geographic hierarchies (Zone: SUR, Area: Chiapas, Sector: 24565, Warehouse: San Cristóbal de las Casas) are **100% synthetic**.
- **Statistical distributions and scoring logic remain identical to the original project**: total client count (1,789), total routes (22), exact score ranges (22.4 to 47.5), and global adoption stage breakdowns.
- Line-by-line verification confirmed that no real client, route code, or proprietary identifier appears in this version.

---

##  Business Problem

Where should commercial and field operations allocate resources to maximize B2B digital adoption across 1,789 clients at different onboarding stages within a specific territory?

---

##  Tech Stack

- **Python (Pandas):** Data cleaning, dataset transformation, and anonymization pipelines.
- **SQL (SQLite):** Multi-table join integration, CTEs, and route-level aggregation (`digital_adoption.db`).
- **Looker Studio:** Executive interactive dashboards, heatmap tables, route score gauges, and conversion funnel charts.
- **Jupyter Notebooks:** Exploratory Data Analysis (EDA), cohort modeling, and documentation.

---

##  Methodology

### 1. Client Segmentation Criteria

Clients are classified into 4 distinct onboarding stages based on their registration status and digital purchasing share (`%_venta_digital`):

| Category (`status_registro` / `categoria`) | Definition / Rule |
| :--- | :--- |
| **pct_no_registrados** | Non-registered clients without an active account in the mobile app |
| **pct_registrados_no_digitales** | Registered clients with an active account but 0% digital sales share |
| **pct_hibridos** | Hybrid clients with 1% – 69% digital purchase share |
| **pct_fully** | Fully digital clients with ≥ 70% digital purchase share |

---

### 2. Weighted Priority Scoring Model (`score_prioridad`)

**Formula:**
$$\text{Score} = (\% \text{Reg. Non-Digital} \times 0.40) + (\% \text{Non-Reg.} \times 0.25) + (\% \text{Hybrids} \times 0.20) + ((100 - \% \text{Fully}) \times 0.15)$$

**Weights Justification:**
- **40% Registered Non-Digital (`pct_registrados_no_digitales`):** Highest priority quick wins (clients already registered who need activation).
- **25% Non-Registered (`pct_no_registrados`):** Acquisition volume (requires account creation + activation).
- **20% Hybrids (`pct_hibridos`):** Scalable accounts (already familiar with the B2B platform).
- **15% Fully Digital Gap (`100 - pct_fully`):** Contextual growth margin.

**Score Scale:** Higher score indicates higher digitalization potential and field route priority.

---

##  Dashboard Features & Funnel Analysis

The interactive dashboard is structured into two main analytical views:

### 1. View 1 — Route Prioritization Dashboard (`Priorización de Rutas - Digitalización`)
- **Territory KPI Cards:** Total Routes (22), Total Clients (1,789), Score Max (47.5), Score Min (22.4), and Average Score Gauge (39.1).
- **Route Heatmap Table:** Tabular breakdown displaying `ruta_sap`, `total_clientes`, percentage shares per category, and a color-scale heatmap on `score_prioridad` (e.g., top priority route `RT019` with a score of 47.5).
- **Territory Selectors:** Dynamic dropdown filters for `ruta_sap` and zone parameters.

### 2. View 2 — Client Universe & Conversion Funnel (`Universo de Clientes X Ruta - Digitalización`)
- **Conversion Funnel Visualization:** A funnel chart detailing client progression across the digital adoption ladder (*No registrados ➔ Registrados no digitales ➔ Híbridos ➔ Fully digital*).
- **Route-Level Bottleneck Identification:** Selecting a route (e.g., `RT001`) dynamically filters the funnel chart and client list, exposing the exact drop-off stage (e.g., routes blocked at initial registration vs. routes with high hybrid retention).
- **Granular Client Table:** Drill-down table listing `cliente_id`, `nombre_cliente`, `%_venta_digital`, `categoría`, and `status_registro` for targeted field execution.

---

## Repository Structure

´´´
text
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
