---
layout: page
title: "Decoding Retail Behavior: An End-to-End Data Pipeline Analysis"
date: 2026-09-14
excerpt: "Taking 541,000+ raw e-commerce transaction lines from Excel, building a relational cleaning infrastructure in PostgreSQL, and deploying an interactive Power BI operational dashboard."
---

<article class="page" style="max-width: 760px; margin: 0 auto; padding: 20px; box-sizing: border-box; display: block; clear: both;">

### 📊 Project Repositories & Full Documentation

To review the complete long-form engineering metrics, full data dictionary tables, and raw script configurations, visit the production spaces directly:

*   **View Full Code & Documentation:** [👉 GitHub Repository Link](https://github.com)
*   **Explore Interactive Dashboard:** [👉 Live Power BI Report](https://powerbi.com)

---

### Executive Summary

This project analyzes **541,909 raw transactions** from a UK-based online gift retailer to uncover underlying revenue drivers, customer behavior metrics, and hidden operational risks. 

Instead of jumping straight into basic charts, I built a reproducible data engineering pipeline: cleaning and modeling the data architecture inside **PostgreSQL**, generating advanced analytics like **RFM Customer Segmentation** and **Market Basket Co-occurrence models**, and deploying a multi-page interactive **Power BI dashboard** powered by dynamic DAX measures.

---

### The Business Problem Matrix

To give this analysis a true commercial edge, I set out to answer a defined set of critical questions across three major business stakeholders:

*   **For the CEO (Revenue & Sales):** Pinpoint exact revenue concentration risks. What percentage of our entire survival relies solely on the UK market? Which specific international regions show the strongest organic signals for local distribution hubs?
*   **For the Marketing Director (Audience Retention):** Calculate our actual customer lifetime value. How many shoppers buy once versus returning? Who represents the upper 10% VIP spending tier, and when are they active during the week to optimize promotional campaign scheduling?
*   **For the Operations Manager (Inventory & Logistics):** Isolate fulfillment leaks. Which inventory items carry massive cancellation rates? What is our real typical order profile once bulk anomalies are smoothed out? Which items are routinely bought together to fuel cross-selling recommendation features?

---

### Data Pipeline & Cleaning Infrastructure (SQL)

The raw source dataset arrived with structural challenges: 135,080 rows missing customer IDs, over 9,000 explicit order cancellations, and random ledger errors like zero-pound giveaways and negative product quantities. 

To ensure the source data remained completely untampered with and auditable, I built a dedicated relational SQL View called `cleaned_transactions` to execute all transformations programmatically:

```sql
DROP VIEW IF EXISTS cleaned_transactions;

CREATE VIEW cleaned_transactions AS
SELECT
    t.invoice_no,
    t.stock_code,
    COALESCE(t.description, 'UNKNOWN') AS description,
    t.quantity,
    t.invoice_date,
    t.unit_price,
    t.customer_id,
    t.country,
    (t.quantity * t.unit_price) AS revenue,
    -- Transaction behavioral flags
    CASE WHEN t.invoice_no LIKE 'C%' THEN TRUE ELSE FALSE END AS is_cancellation,
    CASE WHEN t.quantity < 0 THEN TRUE ELSE FALSE END AS is_return,
    -- Operational overhead tracking flag
    CASE
        WHEN t.stock_code IN ('POST', 'DOT', 'M', 'D', 'C2', 'BANK CHARGES', 'AMAZONFEE', 'CRUK', 'S', 'B')
        THEN TRUE
        ELSE FALSE
    END AS is_non_product
FROM raw_transactions t
WHERE t.unit_price > 0;
```

#### Strategic Cleaning Choices:
1.  **Cancellations Retained & Flagged:** Rather than washing away returns, I isolated them into true boolean flags (`is_cancellation`), allowing the business to calculate cancellation volume rates as a unique financial vector.
2.  **Overhead Tracking:** Non-product ledger rows like `POSTAGE` and `BANK CHARGES` were flagged so they could be filtered out of product popularity rankings while keeping our overall cash balances accurate.

---

### Advanced Analytical Models

#### 1. RFM Customer Segmentation
Using SQL window functions (`NTILE`), I segmented our customer base across Recency, Frequency, and Monetary scores, mapping them into clear behavioral tiers: Champions, Loyal, At Risk, and Lost.

#### 2. Market Basket Co-occurrence Mining
To drive warehouse optimization and cross-selling features, I built a co-occurrence query inside PostgreSQL that calculated the exact count of unique invoices containing distinct pairs of product codes, identifying high-frequency items bought together.

---

### Dashboard Data Modeling & DAX Layer

I extracted the processed views from PostgreSQL and loaded them into Power BI using a clean **Star Schema** layout: a centralized `cleaned_transactions` fact table linked directly to custom `Date` and `rfm_customers` dimension tables. 

To make the report dynamic, I avoided hardcoded numbers and built a robust calculated DAX layer:

*   **True Revenue Baseline:** `Total Revenue = SUM(cleaned_transactions[revenue])`
*   **Typical Purchase Profiling:** By comparing `Average Order Value` against an explicit `Median Order Value` model using `MEDIANX`, I eliminated the upward skew caused by wholesale bulk buyers, giving leadership an accurate look at a typical B2C transaction.
*   **Exposure Calculation:** Created dynamic filter dimensions like `% Revenue UK` to instantly isolate single-market dependence.

---

### Headline Strategic Insights

*   **Massive Geographic Concentration:** An overwhelming **84.03% of total revenue is locked entirely within the UK**. If a local economic downturn strikes, the business has very little insulation. The Netherlands, Ireland, and Germany represent the strongest international footholds to expand into.
*   **Retention is the True Growth Engine:** A massive **65.58% of our audience are repeat customers**, generating **£7.79M of overall sales value** compared to a small fraction from one-time shoppers. 
*   **Severe Revenue Concentration:** A tiny elite circle of **434 VIP spenders (the top 10% tier) generates a massive 61.38% of total revenue**. Retaining these specific individuals through a VIP loyalty ecosystem is mission-critical.
*   **Operational Time Constraints:** System traffic and shipping orders aggressively cluster on **Thursdays around 12:00 noon**. This directly indicates exactly when the company needs peak warehouse fulfillment staffing and customer support active.

---

### The Big Picture Takeaway

When you stop looking at data metrics one by one and connect them, a massive strategic truth surfaces: **This business is highly concentrated almost everywhere you look.** 

Most revenue relies on one country. Most value relies on a tiny pocket of repeat buyers. Most weekly transaction traffic relies on a tiny multi-hour window on Thursdays. While the current top-line numbers look successful on paper, the lack of diversification means any disruption to that core customer base or peak operational window presents a serious risk.

---

### What I Learned & Challenges Overcome
*   **The "Data Ghost" Problem:** Discovered that Hong Kong generated high revenue numbers but showed zero registered customers. Investigation confirmed that all Hong Kong orders were executed as guest checkouts with no recorded customer IDs—proving that metrics can be correct on paper but highly misleading without proper analysis.
*   **Mean vs. Median Distributions:** The raw average order value looked high (£494.10) but comparing it to the median order value (£303.84) exposed that a tiny pocket of wholesale bulk buyers was inflating the average, proving why checking statistical distribution symmetry is vital.

</article>