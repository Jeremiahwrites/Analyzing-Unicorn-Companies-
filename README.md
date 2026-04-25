# 🦄 Analyzing Unicorn Companies (SQL Project)

## 📌 Project Overview

High-growth private startups valued at **$1 billion+**—commonly called **unicorns**—are strong indicators of where future market leaders may emerge.

This project analyzes unicorn company trends between **2019 and 2021** to help an investment firm identify:

* Which industries are creating the most unicorns
* Where investor momentum is increasing fastest
* Which sectors command the highest valuations
* How portfolio strategy should adapt to market shifts

Using SQL, I explored a multi-table relational database containing company, funding, date, and industry data.

---

## 🗂️ Dataset Structure

The database consists of four tables:

| Table        | Description                            |
| ------------ | -------------------------------------- |
| `companies`  | Company name, city, country, continent |
| `dates`      | Unicorn join date and founding year    |
| `funding`    | Valuation, funding raised, investors   |
| `industries` | Industry classification                |

---

## 🎯 Business Objective

The investment firm wanted answers to one critical question:

> **Which industries are producing the highest number of unicorns, and how valuable are they becoming over time?**

To answer this, I focused on the **Top 3 industries by total unicorn count** and examined their yearly performance from **2019–2021**.

---

## 🧠 SQL Strategy

The analysis used:

* `CTE (WITH clause)` to isolate top industries
* `JOINs` across multiple tables
* `COUNT()` to measure unicorn creation rate
* `AVG()` to evaluate valuations
* `EXTRACT(YEAR FROM date)` for time-series grouping
* `ROUND()` for readable billion-dollar values

---

## 💻 SQL Query

```sql
WITH top_industries AS (
    SELECT i.industry,
           COUNT(*) AS total_unicorn
    FROM industries AS i
    JOIN dates AS d
        ON i.company_id = d.company_id
    GROUP BY i.industry
    ORDER BY total_unicorn DESC
    LIMIT 3
)

SELECT i.industry,
       EXTRACT(YEAR FROM d.date_joined) AS year,
       COUNT(*) AS num_unicorns,
       ROUND(AVG(valuation/1000000000), 2) AS average_valuation_billions
FROM industries AS i
JOIN dates AS d
    ON i.company_id = d.company_id
JOIN funding AS f
    ON i.company_id = f.company_id
JOIN top_industries AS t
    ON i.industry = t.industry
WHERE EXTRACT(YEAR FROM d.date_joined) IN (2019, 2020, 2021)
GROUP BY i.industry, year
ORDER BY year DESC, num_unicorns DESC;
```

---

# 📊 Key Findings

## Top 3 Unicorn-Producing Industries

1. **Fintech**
2. **Internet Software & Services**
3. **E-commerce & Direct-to-Consumer**

These sectors dominated unicorn creation globally.

---

## 📈 2021 Explosion in Unicorn Formation

| Industry                     | Unicorns Created | Avg Valuation ($B) |
| ---------------------------- | ---------------- | ------------------ |
| Fintech                      | 138              | 2.75               |
| Internet Software & Services | 119              | 2.15               |
| E-commerce                   | 47               | 2.47               |

### Insight:

2021 saw a massive spike in unicorn births across all three industries, likely driven by:

* Low interest rates
* Strong venture capital activity
* Accelerated digital transformation after COVID-era shifts
* Massive adoption of online finance, remote tools, and ecommerce

---

## 💰 Highest Valuations Came Earlier

| Year | Industry          | Avg Valuation ($B) |
| ---- | ----------------- | ------------------ |
| 2019 | Fintech           | 6.80               |
| 2020 | Internet Software | 4.35               |
| 2020 | Fintech           | 4.33               |

### Insight:

While 2021 produced the most unicorns, **average valuations were lower** than previous years.

This suggests:

* More startups reached $1B status
* But fewer became mega-unicorns immediately
* Investor capital spread across more companies instead of fewer giants

---

## 🧠 Investor Intelligence

## 1️⃣ Fintech is the strongest long-term bet

* Highest unicorn count in 2021
* Highest historical valuations
* Strong global adoption in payments, lending, banking tech

### Recommendation:

Increase exposure to:

* Embedded finance
* Cross-border payments
* Insurtech
* SME lending platforms

---

## 2️⃣ Internet Software remains scalable

119 unicorns in 2021 proves demand for:

* SaaS tools
* Cloud infrastructure
* Cybersecurity
* Workflow automation

### Recommendation:

Focus on B2B SaaS and AI-enabled software firms.

---

## 3️⃣ E-commerce is stabilizing

Strong growth, but lower counts than Fintech and Software.

### Recommendation:

Look for profitable niches:

* Logistics tech
* Social commerce
* Vertical marketplaces

---

# 📌 Strategic Conclusion

The data reveals a major truth:

> **The industries creating the most unicorns are not always the ones with the highest valuations.**

That means smart investors should balance:

* **Growth sectors** → Fintech, SaaS
* **High-value targets** → Mature fintech leaders
* **Emerging efficiency plays** → Specialized ecommerce models

---

# 🛠️ Skills Demonstrated

* SQL Joins
* CTEs
* Aggregation
* Business Intelligence
* Trend Analysis
* Investment Insight Generation
* Data Storytelling

---

# 🚀 About This Project

This project was completed as part of a real-world SQL analytics case study focused on venture capital and startup intelligence.

If you found this useful, feel free to ⭐ the repository.

---
