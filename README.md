# Green Cart Ltd — Q2 Performance Analysis

## Project Overview

An end-to-end data analytics project analysing Green Cart Ltd’s Q2 sales performance using customer, product and sales transaction data.

The project was originally completed as part of an Uptrail data analytics project and has been refined into a portfolio-ready analysis, with greater emphasis on data quality, reproducibility, analytical accuracy and business interpretation.

The analysis explores:

- Product and category revenue performance
- Regional sales performance
- Customer value by loyalty tier
- Discounting and quantity purchased
- Delivery delays
- Customer signup-to-first-recorded-order behaviour
- Identification of potentially underperforming orders

---

## Business Questions

1. Which product categories generate the most revenue, and how does performance vary by region?
2. Do discounts influence the quantity of products sold?
3. Which loyalty tier generates the greatest customer value?
4. Are particular regions or product categories experiencing higher delivery delays?
5. Does the time between customer signup and their first recorded order relate to purchasing behaviour?
6. Which orders show a combination of low quantity, high discount and delayed delivery?

---

## Data

The analysis uses three datasets:

| Dataset | Description |
|---|---|
| `customer_info.csv` | Customer demographics, signup dates, regions and loyalty tiers |
| `product_info.csv` | Product information, categories, prices and suppliers |
| `sales_data.csv` | Sales transactions, quantities, prices, discounts, delivery and payment information |

The sales dataset contains approximately 3,000 transactions.

---

## Analytical Workflow

The project follows an end-to-end data analytics workflow:

1. Data loading and initial inspection
2. Data quality assessment
3. Data cleaning and standardisation
4. Customer and product data integration
5. Feature engineering
6. Exploratory data analysis
7. Business-focused analysis
8. Identification of underperforming orders
9. Business interpretation
10. Recommendations

---

## Data Quality & Cleaning

The datasets contained several quality issues that were identified and addressed during the analysis.

Key issues included:

- Missing transaction fields
- Missing customer and product identifiers
- Customer IDs appearing in sales but not in the customer master
- Missing or invalid dates
- Inconsistent categorical labels and spelling
- Delivery status inconsistencies
- Payment method inconsistencies
- Missing discount values
- Duplicate order IDs with differing transaction attributes

Rather than automatically removing or imputing problematic records, the analysis distinguishes between:

- Missing values
- Unknown values
- Valid zero values
- Data-quality inconsistencies

Customer and product datasets were integrated with the sales data using their respective identifiers.

Regional information from the sales and customer datasets was retained separately because the two fields represent different attributes.

---

## Feature Engineering

Several analytical features were created to support the business analysis.

### Revenue

Transaction revenue was calculated as:

`Quantity × Unit Price × (1 − Discount)`

Missing discount values were not automatically treated as zero.

### Price Band

Products were grouped into analytical price bands:

- Low
- Medium
- High

These bands were based on the distribution of product base prices and are analytical groupings rather than official company classifications.

### Signup-to-Order Timing

The number of days between customer signup and their first recorded order date was calculated.

Timing groups were created:

- Early
- Developing
- Established
- Long-term

### Delivery Delay

A binary `is_late` indicator was created from delivery status.

### Underperforming Orders

An analytical `underperforming` flag was created for orders meeting all three conditions:

- Quantity ≤ 2
- Discount ≥ 15%
- Delivery was delayed

This flag is an analytical definition created for this project and is not a company-provided classification.

---

# Key Findings

## 1. Cleaning was the strongest revenue-generating category

Cleaning generated approximately **£75.4k**, representing **38.92%** of identified-category revenue.

Storage was the second-largest category at approximately **19.72%**.

Cleaning therefore represents a major revenue driver and an important category for inventory, supplier and operational planning.

---

## 2. South recorded the highest average revenue per order

Regional analysis showed:

| Region | Average Revenue per Order |
|---|---:|
| South | £67.66 |
| West | £67.45 |
| East | £65.01 |
| Central | £62.04 |
| North | £61.84 |

South generated the highest average revenue per order, while North and Central had relatively high order volumes but lower average order values.

This suggests that differences in regional revenue are influenced not only by order volume but also by average order value.

---

## 3. Gold customers generated the largest share of loyalty-tier revenue

Gold customers generated approximately **£110.1k**, representing **56.69%** of recorded loyalty-tier revenue.

Average revenue per order was:

- Gold: **£65.60**
- Silver: **£65.27**
- Bronze: **£62.66**

Gold customers contributed the largest total revenue largely because of their larger customer/order base rather than a substantially higher average order value.

---

## 4. Discounts showed no clear relationship with quantity purchased

Average quantity remained close to three units across the recorded discount levels.

| Discount | Average Quantity |
|---|---:|
| 0% | 2.96 |
| 5% | 3.08 |
| 10% | 2.98 |
| 15% | 2.96 |
| 20% | 3.00 |

The 5% discount level recorded the highest average quantity at approximately **3.08 units**.

Overall, the analysis does not provide evidence of a clear relationship where larger discounts consistently result in higher quantities purchased.

---

## 5. Delivery delays varied by region and category

### Regional delay rates

| Region | Delay Rate |
|---|---:|
| East | 41.69% |
| North | 39.27% |
| Central | 38.97% |
| South | 38.59% |
| West | 37.16% |

East recorded the highest delivery delay rate, while West recorded the lowest.

### Category delay rates

| Category | Delay Rate |
|---|---:|
| Personal Care | 41.39% |
| Cleaning | 41.20% |
| Kitchen | 40.45% |
| Outdoors | 37.20% |
| Storage | 34.49% |

Personal Care recorded the highest category-level delay rate, while Cleaning also showed a high delay rate and had the largest number of delayed orders because of its much larger order volume.

---

## 6. Underperforming orders were concentrated in specific areas

Using the analytical definition of:

- Quantity ≤ 2
- Discount ≥ 15%
- Delayed delivery

**154 orders**, representing **5.13%** of classifiable transactions, met all three conditions.

### By category

Cleaning had the highest underperformance rate among the major categories:

**5.98%**

### By region

North recorded the highest regional underperformance rate:

**5.78%**

### Region × Category

Among combinations with at least 100 orders:

- **Central × Storage:** 8.18% underperformance rate
- **North × Cleaning:** 7.35%
- **South × Cleaning:** 6.90%
- **West × Cleaning:** 6.72%

North × Cleaning is particularly important operationally because it combines an elevated rate with meaningful transaction volume, accounting for **18 flagged orders out of 245**.

Cleaning products also appeared frequently among the products associated with underperforming orders.

---

## 7. Signup timing did not show a clear relationship with first-purchase value

The customer-level analysis examined the number of days between signup and the customer's first recorded order date.

The analysis found no clear evidence that customers who waited longer after signup generated higher-value first purchases.

Average first-day revenue by timing group was approximately:

| Timing Group | Average First-Day Revenue |
|---|---:|
| Early | £391.32 |
| Developing | £396.92 |
| Established | £391.39 |
| Long-term | £377.82 |

Developing customers recorded the highest average first-day revenue, while Long-term customers recorded the lowest.

The difference between groups was relatively small, so the results do not support a strong relationship between longer signup-to-order timing and higher first-purchase value.

---

# Business Recommendations

### 1. Protect and strengthen Cleaning performance

Cleaning is the largest revenue-generating category. Inventory planning, supplier management and product availability should therefore receive particular attention.

### 2. Investigate delivery delays

East recorded the highest regional delay rate, while Personal Care and Cleaning showed the highest category-level delay rates.

These areas should be investigated further to identify potential operational causes.

### 3. Prioritise North–Cleaning

North–Cleaning showed an elevated underperformance rate combined with meaningful order volume.

This combination should be prioritised for deeper operational review.

### 4. Review discount effectiveness

Higher discounts did not consistently correspond with higher quantities purchased.

Discount strategies should therefore be evaluated using actual incremental sales or revenue impact rather than assuming that larger discounts automatically increase demand.

### 5. Monitor customer conversion timing

Signup-to-first-order timing did not show a clear relationship with first-purchase value.

Further analysis could investigate strategies designed to encourage customers to make their first purchase earlier after signup.

---

# Analytical Limitations

Several limitations should be considered when interpreting the findings.

### Same-day order dates

All valid order dates in the dataset fall on the same day.

Therefore, the analysis refers to the **first recorded order date/day** rather than claiming to identify the exact first transaction within the day.

### Missing discount values

Missing discount values were not automatically converted to zero because missing does not necessarily mean that no discount was applied.

### Revenue vs profitability

Revenue was calculated from transaction quantity, price and discount.

The dataset does not provide sufficient cost or margin information to determine true product profitability.

### Underperformance definition

The underperforming-order flag is an analytical definition created for this project.

It identifies potentially concerning combinations of characteristics but does not establish that an order was commercially unprofitable.

### No causal inference

The analysis identifies relationships and patterns within the available data.

It does not establish that discounts caused changes in quantity, or that a particular region directly caused delivery delays.

### Limited time period

The analysis represents a Q2 snapshot and should be supplemented with longer-term data before making major strategic decisions.

---

# Tools & Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

---

# Project Structure

```text
Green-Cart-Q2-Performance-Analysis/
│
├── README.md
├── Green_Cart_Q2_Performance_Analysis.ipynb
│
├── data/
│   ├── customer_info.csv
│   ├── product_info.csv
│   └── sales_data.csv
│
└── visualisations/
    ├── category_performance.png
    ├── regional_performance.png
    ├── loyalty_performance.png
    ├── discount_quantity.png
    ├── delivery_performance.png
    └── underperforming_orders.png<img width="590" height="373" alt="Screenshot 2026-09-01 135721" <img width="590" height="373" alt="Screenshot 2026-09-01 135721" src="https://github.com/user-attachments/assets/8a94c358-2362-471f-9430-f31a245030b3" />
<img width="482" height="368" alt="Screenshot 2026-09-01 183844" src="https://github.com/user-attachments/assets/600f2206-7601-4aa5-8fe8-5989ae7f09b1" />
<img width="595" height="362" alt="Screenshot 2026-09-01 181759" src="https://github.com/user-attachments/assets/7710b4e1-97db-4345-8293-415f3d90d9f6" />
<img width="476" height="320" alt="Screenshot 2026-09-03 140802" src="https://github.com/user-attachments/assets/05191601-79eb-4a5c-9e14-9d1dee4512c7" />

