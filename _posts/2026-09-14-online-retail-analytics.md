---
layout: project-slides
title: "Decoding Retail Behavior: An End-to-End Pipeline"
title: "Decoding Retail Behavior: An End-to-End Data Pipeline Analysis"
date: 2026-09-14
excerpt: "Taking 541,000+ raw e-commerce transaction lines from Excel, building a relational cleaning infrastructure in PostgreSQL, and deploying an interactive Power BI operational dashboard."
---

### Executive Summary

This project analyzes **541,909 raw transactions** from a UK-based online gift retailer to identify overall revenue drivers, target customer values, and core operational risks. 

Data was programmatically cleaned and modeled inside a relational **PostgreSQL** database, then deployed out into **Power BI** utilizing custom DAX measures across a dynamic multi-page dashboard application.

### The Business Problem Matrix

To give this analysis a true commercial edge, I set out to answer a defined set of performance questions across three core business stakeholder roles:

* **CEO (Revenue & Sales Performance):** Pinpoint exact market concentration risks. What percentage of our entire survival relies solely on the UK market? Which specific international regions show the strongest organic signals for local distribution hubs?
* **Marketing Director (Customer Behavior):** Calculate our actual customer lifetime value footprint. How many shoppers buy once versus returning? Who represents our top 10% VIP spending tier, and when are they active during the week?
* **Operations Manager (Inventory & Logistics):** Isolate hidden fulfillment friction. Which inventory items carry massive cancellation rates? What is our real typical order profile once bulk anomalies are smoothed out? Which items are routinely bought together?

### Data Pipeline & Cleaning Infrastructure (SQL)

The raw source dataset arrived with significant data quality challenges: **135,080 rows missing customer IDs**, over **9,000 explicit order cancellations**, and random ledger adjustments like zero-pound giveaways and negative product quantities. 

To ensure the source data remained completely untampered with and auditable, I built a dedicated relational SQL View called `cleaned_transactions` to handle all transformations programmatically:

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
    CASE 
        WHEN t.invoice_no LIKE 'C%' THEN TRUE 
        ELSE FALSE 
    END AS is_cancellation,
    CASE 
        WHEN t.quantity < 0 THEN TRUE 
        ELSE FALSE 
    END AS is_return,
    -- Operational overhead tracking flag
    CASE
        WHEN t.stock_code IN (
            'POST', 'DOT', 'M', 'D', 'C2', 
            'BANK CHARGES', 'AMAZONFEE', 'CRUK', 
            'S', 'B'
        ) THEN TRUE
        ELSE FALSE
    END AS is_non_product
FROM raw_transactions t
WHERE t.unit_price > 0;
```

#### Strategic Cleaning Choices:
1. **Cancellations Retained & Flagged:** Rather than washing away returns, I isolated them into true boolean flags (`is_cancellation`), allowing the business to calculate cancellation volume rates as a unique financial vector.
2. **Overhead Tracking:** Non-product ledger rows like `POSTAGE` and `BANK CHARGES` were flagged so they could be filtered out of product popularity rankings while keeping our overall cash balances accurate.

### Advanced Analytical Models

* **RFM Customer Segmentation:** Scored customers across Recency, Frequency, and Monetary tiers using SQL window functions (`NTILE`), grouping accounts into clear behavioral segments (Champions, Loyal, At Risk, Lost) to guide retention marketing budgets.
* **Market Basket Co-occurrence Mining:** Built a proximity join inside PostgreSQL to calculate the exact frequency of unique invoices containing distinct pairs of product codes, identifying high-frequency item bundles frequently bought together.

### Dashboard Data Modeling & DAX Layer

I extracted the processed relational views from PostgreSQL and loaded them into Power BI using a clean **Star Schema** layout: a centralized `cleaned_transactions` fact table linked directly to custom `Date` and `rfm_customers` dimension tables. 

To build a fully dynamic interactive presentation layer, I developed a robust calculated DAX layer:

* **True Revenue Baseline:** `Total Revenue = SUM(cleaned_transactions[revenue])`
* **Typical Purchase Profiling:** By comparing `Average Order Value` against an explicit `Median Order Value` model using `MEDIANX`, I eliminated the upward skew caused by wholesale bulk buyers, giving leadership an accurate look at a typical B2C transaction.
* **Exposure Calculation:** Created dynamic filter dimensions like `% Revenue UK` to instantly isolate single-market dependence.

### Headline Strategic Insights

* **Massive Geographic Concentration:** An overwhelming **84.03% of total revenue is locked entirely within the UK**. If a local economic downturn strikes, the business has very little insulation. The Netherlands, Ireland, and Germany represent the strongest international footholds to expand into.
* **Retention is the True Growth Engine:** A massive **65.58% of our audience are repeat customers**, generating **£7.79M of overall sales value** compared to a small fraction from one-time buyers. 
* **Severe Revenue Concentration:** A tiny elite circle of **434 VIP spenders (the top 10% tier) generates a massive 61.38% of total revenue**. Retaining these specific individuals through a VIP loyalty ecosystem is mission-critical.
* **Operational Time Constraints:** System traffic and shipping orders aggressively cluster on **Thursdays around 12:00 noon**. This directly indicates exactly when the company needs peak warehouse fulfillment staffing and customer support active.

### The Big Picture Takeaway

When you stop looking at data metrics one by one and connect them, a massive strategic truth surfaces: **This business is highly concentrated almost everywhere you look.** Most revenue relies on one country. Most value relies on a tiny pocket of repeat buyers. Most weekly transaction traffic relies on a tiny multi-hour window on Thursdays. 

While the current top-line numbers look successful on paper, the lack of diversification means any disruption to that core customer base or peak operational window presents a serious risk.

### What I Learned & Challenges Overcome

* **The "Data Ghost" Problem:** Discovered that Hong Kong generated high revenue numbers but showed zero registered customers. Investigation confirmed that all Hong Kong orders were executed as guest checkouts with no recorded customer IDs—proving that metrics can be correct on paper but highly misleading without proper analysis.
* **Mean vs. Median Distributions:** The raw average order value looked high (£494.10) but comparing it to the median order value (£303.84) exposed that a tiny pocket of wholesale bulk buyers was inflating the average, proving why checking statistical distribution symmetry is vital.

### Project Portals & Repositories

<div style="margin: 20px 0; display: flex; flex-direction: row; gap: 15px; align-items: center; justify-content: center; width: 100%; box-sizing: border-box;">
  <a href="https://github.com" target="_blank" rel="noopener noreferrer" style="background-color: #000; color: #fff; padding: 8px 16px; text-decoration: none; border-radius: 4px; font-weight: bold; font-size: 0.95rem; font-family: sans-serif; display: inline-block; white-space: nowrap;">👉 GitHub Repository</a>
  <a href="https://powerbi.com" target="_blank" rel="noopener noreferrer" style="background-color: #000; color: #fff; padding: 8px 16px; text-decoration: none; border-radius: 4px; font-weight: bold; font-size: 0.95rem; font-family: sans-serif; display: inline-block; white-space: nowrap;">📊 Power BI Dashboard</a> 
</div>