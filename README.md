# Green Cart Ltd — Q2 Performance Analysis

## Project Overview

An end-to-end data analytics project analysing Green Cart Ltd's Q2 sales performance using customer, product and sales transaction data.

Originally completed as part of an Uptrail data analytics project, this version has been refined for portfolio use with a stronger focus on data quality, reproducibility, analytical accuracy and business interpretation.

The analysis covers:
- Product and category revenue performance
- Regional sales performance
- Customer value by loyalty tier
- Discounts and quantity purchased
- Delivery delays
- Signup-to-first-recorded-order behaviour
- Potentially underperforming orders

## Business Questions

1. Which product categories generate the most revenue, and how does performance vary by region?
2. Do discounts influence the quantity of products sold?
3. Which loyalty tier generates the greatest customer value?
4. Are particular regions or product categories experiencing higher delivery delays?
5. Does the time between customer signup and their first recorded order relate to purchasing behaviour?
6. Which orders show a combination of low quantity, high discount and delayed delivery?

## Data

| Dataset | Description |
|---|---|
| `customer_info.csv` | Customer demographics, signup dates, regions and loyalty tiers |
| `product_info.csv` | Product information, categories, prices and suppliers |
| `sales_data.csv` | Sales transactions, quantities, prices, discounts, delivery and payment information |

The sales dataset contains approximately 3,000 transactions.

## Analytical Workflow

1. Data loading and initial inspection
2. Data quality assessment
3. Data cleaning and standardisation
4. Customer and product data integration
5. Feature engineering
6. Exploratory data analysis
7. Business-focused analysis
8. Underperformance analysis
9. Business interpretation
10. Recommendations

## Data Quality & Cleaning

The raw datasets contained missing values, inconsistent labels, missing customer and product identifiers, invalid or missing dates, inconsistent delivery and payment labels, missing discounts, and duplicate order IDs with differing transaction attributes.

The analysis avoids blindly deleting records or treating missing values as confirmed zero values.

Missing discount values were retained as missing rather than automatically converted to zero. Customer and product information was integrated with sales using their respective IDs. Sales-region and customer-region fields were retained separately because they represent different attributes.

## Feature Engineering

### Revenue

Transaction revenue was calculated as:

`Quantity × Unit Price × (1 − Discount)`

Revenue remains missing where required inputs are unavailable.

### Price Band

Products were grouped into Low, Medium and High analytical price bands based on the distribution of base prices. These are analytical groupings, not official company pricing tiers.

### Signup-to-Order Timing

The number of days between signup and the customer's first recorded order date was calculated and grouped into Early, Developing, Established and Long-term.

Because all valid order dates occur on the same day, this analysis refers to the first recorded order date/day. Exact transaction sequence within that day cannot be established.

### Delivery Delay

An `is_late` indicator was created from delivery status.

### Underperforming Orders

An analytical `underperforming` flag was created when an order met all three conditions:

- Quantity ≤ 2
- Discount ≥ 15%
- Delivery was delayed

This is a project-defined analytical flag, not a company-provided classification.

# Key Findings

## 1. Cleaning was the strongest revenue-generating category

Cleaning generated approximately **£75.4k**, representing **38.92%** of identified-category revenue. Storage was the second-largest category at approximately **19.72%**.

## 2. South recorded the highest average revenue per order

| Region | Average Revenue per Order |
|---|---:|
| South | £67.66 |
| West | £67.45 |
| East | £65.01 |
| Central | £62.04 |
| North | £61.84 |

South recorded the highest average revenue per order, while North and Central had relatively high order volumes but lower average order values.

## 3. Gold customers generated the largest share of loyalty-tier revenue

Gold customers generated approximately **£110.1k**, representing **56.69%** of recorded loyalty-tier revenue.

Average revenue per order:
- Gold: **£65.60**
- Silver: **£65.27**
- Bronze: **£62.66**

Gold generated the largest total revenue largely because of its larger customer/order base rather than a substantially higher average order value.

## 4. Discounts showed no clear relationship with quantity purchased

| Discount | Average Quantity |
|---|---:|
| 0% | 2.96 |
| 5% | 3.08 |
| 10% | 2.98 |
| 15% | 2.96 |
| 20% | 3.00 |

The 5% discount level recorded the highest average quantity at approximately **3.08 units**. Overall, larger discounts did not consistently correspond to higher purchase quantities.

## 5. Delivery delays varied by region and category

### By region

| Region | Delay Rate |
|---|---:|
| East | 41.69% |
| North | 39.27% |
| Central | 38.97% |
| South | 38.59% |
| West | 37.16% |

### By category

| Category | Delay Rate |
|---|---:|
| Personal Care | 41.39% |
| Cleaning | 41.20% |
| Kitchen | 40.45% |
| Outdoors | 37.20% |
| Storage | 34.49% |

East had the highest regional delay rate. Personal Care had the highest category-level delay rate, while Cleaning had a high delay rate and the largest delayed-order volume.

## 6. Underperforming orders were concentrated in specific areas

**154 orders (5.13% of classifiable transactions)** met the underperformance criteria.

Cleaning had the highest major-category rate at **5.98%**, while North had the highest regional rate at **5.78%**.

Among region-category combinations with at least 100 orders:

| Region–Category | Underperformance Rate |
|---|---:|
| Central — Storage | 8.18% |
| North — Cleaning | 7.35% |
| South — Cleaning | 6.90% |
| West — Cleaning | 6.72% |
| North — Outdoors | 6.60% |

Central–Storage has the highest rate in the volume-filtered analysis. North–Cleaning is an important operational priority because it combines an elevated rate with meaningful volume, with **18 flagged orders out of 245**.

## 7. Signup-to-first-recorded-order timing showed no clear relationship with first-purchase value

| Timing Group | Average First-Day Revenue |
|---|---:|
| Early | £391.32 |
| Developing | £396.92 |
| Established | £391.39 |
| Long-term | £377.82 |

There is no clear evidence that customers who waited longer after signup generated higher-value first purchases.

# Visualisations

### Revenue by Product Category
![Revenue by Product Category](visualisations/category_performance.png)
<img width="488" height="359" alt="Category_performance" src="https://github.com/user-attachments/assets/89855963-f9aa-4f80-a6e8-28ca01dd87ea" />

### Regional Order Volume vs Average Revenue
![Regional Order Volume vs Average Revenue](visualisations/regional_order_volume_vs_average_revenue.png)
<img width="482" height="368" alt="Regional Order Volume vs Average Revenue" src="https://github.com/user-attachments/assets/477e7553-66b0-4e2f-96e6-bec57a7c2c6c" />

### Average Revenue per Order by Region
![Average Revenue per Order by Region](visualisations/regional_average_revenue.png)
<img width="595" height="362" alt="Average Revenue per Order by Region" src="https://github.com/user-attachments/assets/0788702f-ada7-479c-b777-bbee75e11c8c" />

### Revenue by Loyalty Tier
![Revenue by Loyalty Tier](visualisations/loyalty_performance.png)
<img width="442" height="274" alt="Revenue by loyality tier" src="https://github.com/user-attachments/assets/0540e1bb-8a09-4ba8-90da-9d613c8c6ae0" />

### Discount vs Quantity
![Average Quantity by Recorded Discount](visualisations/discount_quantity.png)
<img width="530" height="331" alt="image" src="https://github.com/user-attachments/assets/5a9799f7-b550-4270-8b47-a5cbddf88aba" />

### Delivery Delay Rate by Region
![Delivery Delay Rate by Region](visualisations/delivery_delay_by_region.png)
<img width="439" height="272" alt="Delivery delay by region" src="https://github.com/user-attachments/assets/2afd6239-9c1f-4bab-87ce-7d6986c5b3fd" />

### Delivery Delay Rate by Product Category
![Delivery Delay Rate by Product Category](visualisations/delivery_delay_by_category.png)
<img width="443" height="273" alt="Delivery delay rate by product category" src="https://github.com/user-attachments/assets/ce14cff0-7dfc-40e4-931f-84c883fc02d9" />

### Underperformance Rate by Product Category
![Underperformance Rate by Product Category](visualisations/underperforming_orders_by_category.png)
<img width="441" height="274" alt="Underperformance rate by product category" src="https://github.com/user-attachments/assets/1e2e9923-39cc-4022-b93c-887845aaf3e5" />

### Underperformance Rate by Region
![Underperformance Rate by Region](visualisations/underperforming_orders_by_region.png)
<img width="440" height="275" alt="underperformance rate by region" src="https://github.com/user-attachments/assets/e7762741-a770-44b3-8bd0-08ae22395891" />

### Underperformance by Region–Category
![Underperformance by Region–Category](visualisations/underperforming_region_category.png)
<img width="554" height="382" alt="underperformance rate by region, category combination" src="https://github.com/user-attachments/assets/4c39bed9-a993-44be-9744-eb68fec36c83" />

### Average First-Day Revenue by Purchase Timing
![Average First-Day Revenue by Purchase Timing](visualisations/first_day_revenue_by_purchase_timing.png)
<img width="476" height="320" alt="First_day_revenue_by_purchase_timing" src="https://github.com/user-attachments/assets/8686634f-9c3a-4a38-8991-9b87e3ebc058" />

## Business Recommendations

1. **Protect and strengthen Cleaning performance** through inventory planning, supplier management and availability monitoring.
2. **Investigate delivery delays**, particularly in East and within Personal Care and Cleaning.
3. **Prioritise North–Cleaning** for deeper operational review.
4. **Review discount effectiveness** rather than assuming higher discounts generate higher quantities.
5. **Monitor customer conversion timing** and test strategies that encourage earlier first purchases.

## Analytical Limitations

- All valid order dates occur on the same day, so exact within-day transaction sequence cannot be established.
- Missing discount values were not automatically treated as zero.
- Revenue represents transaction revenue, not profitability, because sufficient cost or margin data is unavailable.
- The underperforming flag is an analytical definition rather than a company classification.
- Underperformance patterns do not establish causal relationships.
- The dataset represents a limited Q2 snapshot.

## Tools & Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

## Project Structure

```text
Green-Cart-Q2-Performance-Analysis/
├── README.md
├── Green_Cart_Q2_Performance_Analysis.ipynb
├── data/
│   ├── customer_info.csv
│   ├── product_info.csv
│   └── sales_data.csv
└── visualisations/
    ├── category_performance.png
    ├── regional_order_volume_vs_average_revenue.png
    ├── regional_average_revenue.png
    ├── loyalty_performance.png
    ├── discount_quantity.png
    ├── delivery_delay_by_region.png
    ├── delivery_delay_by_category.png
    ├── underperforming_orders_by_category.png
    ├── underperforming_orders_by_region.png
    ├── underperforming_region_category.png
    └── first_day_revenue_by_purchase_timing.png
