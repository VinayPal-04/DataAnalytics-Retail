# Retail Analytics

A complete end-to-end retail analytics project
The project analyses chip purchasing behaviour across customer segments and evaluates the commercial impact of a new in-store layout trial using statistical uplift testing.

## Problem Statement
The Category Manager for chips at a major retail client is
preparing a **strategic plan for the next half-year**. She needs data-driven answers to two critical business questions: 

1. **Who is buying chips?** — Which customer segments are driving volume,
   spend, and margin in the chips category?
2. **Did the new store layout work?** — Were the trial stores (77, 86, 88)
   meaningfully more successful after the layout change, and should it be
   rolled out across all stores?

Without rigorous analysis:
- Allocating promotional budget to the wrong segments
- Rolling out an expensive store layout change with no proven ROI
- Missing margin opportunities in underserved premium segments

## What We Solved

| Task | Problem | Solution |
|------|---------|----------|
| Task 1 | No clear picture of who buys chips or what drives spend | Segmented 72,637 customers across 7 lifestages × 3 premium tiers; identified high-value segments |
| Task 2 | No rigorous way to assess if the trial layout actually worked | Built a control store matching algorithm + 95% CI uplift test for stores 77, 86 & 88 |
| Task 3 | Insights needed in a client-ready format | Produced a Quantium-branded PowerPoint report using the Pyramid Principle framework |

## Project Structure

DataAnalytics-Retail/
│
├── data/
│   ├── QVI_purchase_behaviour.csv       # Customer loyalty + segment data
│   └── QVI_transaction_data.xlsx        # Transaction-level chip purchase data
│
├── notebooks/
│   ├── DATA_PREP_AND_CX_ANALYTICS.ipynb # Task 1 — Data prep & customer analytics
│   └── EXPERIMENTATION_AND_UPLIFT.ipynb # Task 2 — Control store selection & uplift testing
│
├── output/
│   └── QVI_Category_Review/
│       └── QVI_Category_Review.pptx     # Task 3 — Final client report (PowerPoint)
│
└── README.md

---

## Tasks Overview

### Task 1 — Data Preparation & Customer Analytics

**Goal:** Understand current purchasing trends and identify which customer
segments drive chips sales.

**Steps:**
- Loaded and merged transaction data with customer purchase behaviour
- Fixed date formats (Excel serial → datetime), removed outlier bulk buyers
- Derived two new features: **Pack Size** (grams from product name) and
  **Brand** (first word of product name, with standardisation map)
- Segmented customers across **7 lifestages** and **3 premium tiers**
- Computed segment-level KPIs: total sales, unique customers, avg
  transactions per customer, avg spend per customer, avg price per unit

**Key Findings:**
- 🏆 **Mainstream Young Singles/Couples** — largest single segment (8,088),
  impulse-driven, highest promotional ROI
- 👴 **Retirees** — largest lifestage overall (14,805 customers), habitual
  buyers, respond to loyalty mechanics and multipacks
- 💰 **Midage Singles/Couples** — highest Premium concentration (33.4%),
  best margin growth opportunity
- 👨‍👩‍👧 **Family segments** (Older & Young Families) — skew heavily Budget
  (43–48%), value packs are the lever

---

### Task 2 — Experimentation & Uplift Testing

**Goal:** Evaluate whether the new chip aisle layout in trial stores 77,
86 and 88 drove a statistically significant improvement in performance.

**Approach:**

1. Aggregate data → monthly store-level metrics
(total sales, unique customers, avg txns per customer)
2. Control Store Selection
├── Pearson correlation  (pre-trial monthly sales similarity)
├── Normalised magnitude distance score
└── Composite score = (corr + dist_score) / 2
→ Highest composite = best control match
3. Uplift Testing (per trial-control pair, per metric)
├── Scale control to trial level using pre-trial ratio
├── Build 95% CI from pre-trial % differences
└── If trial months fall OUTSIDE CI → significant uplift ✅

**Results:**

| Trial Store | Control Store | Sales Uplift Significant? | Primary Driver |
|-------------|---------------|--------------------------|----------------|
| 77 | TBD by algo | Yes | More unique customers |
| 86 | TBD by algo | Yes | More unique customers |
| 88 | TBD by algo | No | No clear driver |

---

### Task 3 — Analytics & Commercial Application

**Goal:** Present findings to Julia in a clear, jargon-free, client-ready
report following Quantium's **Pyramid Principle** framework.

**Deliverable:** A 12-slide PowerPoint deck including:
- Executive Summary
- Category overview with commercial implications
- Affluence × Lifestage segment analysis
- Control store methodology explanation
- Trial results and statistical evidence

## 📊 Key Visualisations

The following charts were produced across Tasks 1 and 2:

- **Customer Count by Lifestage** — horizontal bar chart
- **Premium Tier Donut** — Budget / Mainstream / Premium split
- **Stacked Bar — Tier Mix by Lifestage** — % breakdown per segment
- **Segment Heatmap** — customer count per lifestage × tier cell
- **Control Store Selection Charts** — composite similarity scores
- **Uplift Charts** — trial vs scaled control with 95% CI band
- **Final Summary Table** — significance results + recommendation per store

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3.10+ | Core language |
| Pandas | Data loading, cleaning, merging, aggregation |
| NumPy | Numerical operations, distance scoring |
| Matplotlib | All charts and dashboards |
| SciPy | Pearson correlation for control store selection |
| openpyxl | Reading `.xlsx` transaction data |

---

## 🚀 How to Run

### 1. Clone the repo
```bash
git clone https://github.com/VinayPal-04/DataAnalytics-Retail.git
cd DataAnalytics-Retail
```

### 2. Install dependencies
```bash
pip install pandas numpy matplotlib scipy openpyxl
```

### 3. Run the notebooks

Open in **Jupyter Notebook** or **Google Colab**:

notebooks/DATA_PREP_AND_CX_ANALYTICS.ipynb   → Task 1
notebooks/EXPERIMENTATION_AND_UPLIFT.ipynb   → Task 2

> **Note:** Upload both data files from the `/data` folder when prompted
> in Colab, or ensure they are in the working directory for local runs.

---

