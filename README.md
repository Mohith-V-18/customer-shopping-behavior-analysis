#  Customer Shopping Behavior Analysis

An end-to-end data analysis project on 3,900 retail transactions — covering data cleaning in **Python**, business queries in **PostgreSQL**, and an interactive dashboard in **Power BI**.

---

##  Project Overview

This project analyzes customer shopping behavior to uncover insights into:
- Spending patterns across gender and age groups
- Product ratings and discount dependency
- Subscription behavior vs. purchase frequency
- Customer segmentation (New / Returning / Loyal)

---

##  Dataset

| Attribute | Details |
|-----------|---------|
| Records | 3,900 transactions |
| Features | 18 columns |
| Missing Values | 37 nulls in `Review Rating` |
| Categories | Clothing, Accessories, Footwear, Outerwear |

**Key columns:** `age`, `gender`, `category`, `item_purchased`, `purchse_amount`, `review_rating`, `discount_applied`, `subscription_status`, `previous_purchases`, `shipping_type`, `age_groups`, `purchase_frequency`

---

##  Tech Stack

| Tool | Purpose |
|------|---------|
| Python (pandas) | Data cleaning & EDA |
| PostgreSQL | Business query analysis |
| SQLAlchemy / psycopg2 | Python → DB integration |
| Power BI Desktop | Interactive dashboard |
| Jupyter Notebook | Development environment |

---

##  Repository Structure

```
customer-shopping-behavior-analysis/
├── data/
│   └── customer_shopping_behavior.csv
├── notebooks/
│   └── customer_shopping.ipynb
├── sql/
│   └── customer_shopping_sql1.sql
├── dashboard/
│   └── customer_shopping.pbix
├── reports/
│   └── Customer_Shopping_Behavior_Analysis.pdf
└── README.md
```

---

##  Python — Data Preparation

Steps performed in `customer_shopping.ipynb`:

1. **Load & explore** — `df.info()`, `df.describe()`, `df.isnull().sum()`
2. **Impute missing values** — Median Review Rating per product category
3. **Standardize columns** — snake_case rename; `purchase_amount_(usd)` → `purchse_amount`
4. **Feature engineering:**
   - `age_groups` — custom bins `[0, 18, 30, 55, 100]` → `Young / Adults / Middle-Aged / Seniors`
   - `purchase_frequency` — text labels mapped to numeric days
5. **Drop redundant column** — `discount_applied == promo_code_used` → dropped `promo_code_used`
6. **Load to PostgreSQL** — via SQLAlchemy into `customer_shopping_behavior` database

---

##  SQL — Business Questions

| # | Question | Key Result |
|---|----------|-----------|
| Q1 | Revenue by gender | Male: $157,890 · Female: $75,191 |
| Q2 | Discount users above average spend | 839 customers |
| Q3 | Top 5 products by rating | Gloves (3.86), Sandals (3.84), Boots (3.82) |
| Q4 | Shipping type vs. avg spend | Express: $60.48 · Standard: $58.46 |
| Q5 | Subscribers vs. non-subscribers | Similar avg spend (~$59) |
| Q6 | Most discount-dependent products | Hat (50%), Sneakers (49.66%) |
| Q7 | Customer segmentation | Loyal: 3,116 · Returning: 701 · New: 83 |
| Q8 | Top 3 products per category | Jewelry, Blouse, Sandals, Jacket lead |
| Q9 | Repeat buyers & subscriptions | 72% of repeat buyers not subscribed |
| Q10 | Revenue by age group | Middle-Aged dominates total revenue |

---

##  Power BI Dashboard

**KPIs:** 3,900 customers · $59.76 avg purchase · 3.75 avg rating · 27% subscription rate

**Slicers:** Subscription Status · Gender · Category · Shipping Type

**Charts:** Subscription donut · Revenue by category · Sales by category · Revenue & sales by age group

---

##  Key Insights

- Male customers generate **~2.1× more revenue** than female customers
- **79.9% of customers are Loyal** — strong retention base
- **72% of repeat buyers are not subscribed** — top conversion opportunity
- Hat has a **50% discount rate** — highest margin risk
- Middle-Aged (30–55) leads total revenue due to the widest age bracket
- Average spend is nearly equal across subscribed and non-subscribed customers

---

##  Business Recommendations

| Priority | Recommendation |
|----------|---------------|
| 🔴 High | Target repeat buyers with subscription campaigns |
| 🔴 High | Feature Gloves, Sandals, Boots in marketing |
| 🟡 Medium | Review discount strategy for Hat & Sneakers |
| 🟡 Medium | Build loyalty rewards to convert Returning → Loyal |
| 🟢 Low | Targeted content for Adults (18–30) segment |

---

##  How to Run

**1. Clone the repo**
```bash
git clone https://github.com/<your-username>/customer-shopping-behavior-analysis.git
cd customer-shopping-behavior-analysis
```

**2. Install Python dependencies**
```bash
pip install pandas sqlalchemy psycopg2-binary
```

**3. Run the notebook**
```bash
jupyter notebook notebooks/customer_shopping.ipynb
```
> Update the DB password in the connection string before running.

**4. Run SQL queries**
```bash
psql -U postgres -d customer_shopping_behavior -f sql/customer_shopping_sql1.sql
```

**5. Open the dashboard**

Open `dashboard/customer_shopping.pbix` in Power BI Desktop and refresh the data source.

---


