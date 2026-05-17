# Quantitative Mirror Trade Discrepancy Analysis (TBML)

> **Analytical Track:** Bilateral Data Pipelines & Anomaly Detection
> 
> **Regulatory Anchor:** MAS Notice 626 (Paragraph 4 & Red Flag Indicators) | FATF TBML Guidance
> 
> **Project Status:** In Progress (Phase 1: Environment & Architecture)

---

## I. Strategic Context & Architecture

This repository contains the end-to-end analytical pipeline designed to identify systematic financial crime risks disguised within legitimate international commercial channels. By interrogating reporting asymmetries across key South Asian and Southeast Asian trading corridors, this project transitions Trade-Based Money Laundering (TBML) detection from legacy, rule-based heuristics into data-driven anomaly modeling.


              [ UN Comtrade API ] ──> ( Pulls Bilateral Flows )
                                             │
                                             ▼
           [ CIF / FOB Re-balancing ] ──> ( Normalizes Shipping Gaps )
                                             │
                                             ▼
     [ Multi-Year Persistence Filter ] ──> ( Triggers Anomaly Flags >25% )
                                             │
                                             ▼
         [ Analytical Visualizations ] ──> Heatmaps & Time-Series Notebooks


### Repository Blueprints
* `notebooks/`: Modular data acquisition, cleaning pipelines, and quantitative calculation engines.
* `data/`: Local storage caches for sanitized commodity records mapped by UN M49 specifications.
* `outputs/`: High-impact graphic matrixes illustrating systemic corridor friction.
* `docs/`: Regulatory mapping schemas aligning data-derived outliers to actionable compliance alerts.

---

## II. Pipeline Methodology & Mathematics

The fundamental core of this project relies on a multi-layer ingestion engine built with Python and pandas to evaluate reporting variances.

### 1. Automated Extraction
Data is systematically compiled using the `comtradeapicall` SDK layer, extracting primary annual statistics across 8–10 highly specific cross-border trading lanes using Harmonized System (HS) commodity groups (specifically Targeting Electronics, Textiles, and Precious Metals).

### 2. Discrepancy Equation
The pipeline normalizes the mathematical delta resulting from mismatched reporting terms—such as Export figures captured as **FOB** (Free on Board) contrasting against incoming Import metrics logged via **CIF** (Cost, Insurance, Freight):

$$\text{Discrepancy Ratio} = \frac{\text{Value}_{\text{Import (Country B) [CIF]}}}{\text{Value}_{\text{Export (Country A) [FOB]}} \times (1 - \delta_{\text{fright/insur}})}$$

### 3. Persistent Risk Triggering
A normal random variation is immediately discarded. Outliers are filtered using custom tracking thresholds: a corridor is flagged for human intervention only when the discrepancy factor breaches **>25%** consistently across a rolling window of **3 consecutive calendar years**.

---

## III. Execution Instructions

### Technical Core
* Language: Python 3.11+
* Primary Libraries: `pandas`, `numpy`, `comtradeapicall`, `seaborn`, `matplotlib`

### Getting Started
To prepare your environment, install the direct UN API client wrapper:
```bash
pip install comtradeapicall
