# Causal Impact of Weekend Staffing Reallocation on Conversion Rate

**Domain:** Retail operations / HR planning  
**Method:** Difference-in-Differences (DiD) with Wasserstein-matched control group  
**Stack:** Python · pandas · numpy · seaborn · matplotlib · scipy · scikit-learn

> **Note on data** The datasets in `data/` are **synthetic**. They were generated to replicate the structure, distributions and statistical patterns of a real Difference-in-Differences analysis — without exposing any proprietary or confidential information.

> Follow-up to [`staffing-conversion-rate-analysis`](https://github.com/marcomorabito94-mm/staffing-conversion-rate-analysis), which identified the staffing→CR correlation and the store-level opportunity.

---

## Context

A previous study identified a positive correlation between weekend afternoon staffing coverage and conversion rate across the store network. **Forlì** — flagged among the five stores with the highest incremental potential — redistributed its existing weekend shift hours toward the 12–17 window, with no additional headcount.

## Approach

1. **Control group selection** — 10 stores matched to Forlì via Wasserstein distance on pre-period distribution of hours worked, staffing coverage, and CR across all 47 stores in the network. Forlì sits at the 50th percentile of the control group CR distribution.
2. **Parallel trends validation** — KDE comparison confirms control group closely mirrors Forlì in the pre-period
3. **DiD estimation** — per slot: Variant Δ − Control Δ. Control stores show near-zero CR drift (−0.14pp to +0.16pp), validating the design.
4. **Economic quantification** — incremental revenue = DiD CR × post-period traffic × AOV

## Key results

| Slot | ΔStaff DiD | ΔCR DiD | Incremental revenue |
|---|---|---|---|
| Morning 8–11 | −1.17 | +0.64pp | €1,685 |
| Lunch 12–14 | +3.44 | +1.31pp | €2,424 |
| **Afternoon 15–17** | **+3.60** | **+2.94pp** | **€5,429** |
| Evening 18–close | −1.53 | +0.61pp | €966 |
| **TOTAL** | | **+1.37pp** | **€10,504** |

Zero additional headcount. 7 weekends (Nov 15 – Dec 31).

## Repo structure

```
├── data/
│   ├── variant_store.csv           # synthetic data — Forlì (treated store)
│   ├── all_stores_did.csv          # Forlì + 10 matched control stores
│   └── all_stores_background.csv   # all 47 stores (KDE comparison)
├── outputs/
│   ├── 01_staff_distribution.png
│   ├── 02_control_selection.png
│   └── 03_did_by_slot.png
├── did_staffing_intervention.ipynb
└── README.md
```

## How to run

```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn
jupyter notebook did_staffing_intervention.ipynb
```
