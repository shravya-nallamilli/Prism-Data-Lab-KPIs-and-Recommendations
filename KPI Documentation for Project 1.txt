# KPI Documentation

## PRISM DATA LAB TEAM
**Harini, Shravya, Mar**

### Documentation Overview
Define and document the metrics that will be showcased in your dashboard. Clearly outline the calculations and data sources used to derive each metric.

**All calculations have been done for the time period 2020-2021.**

---

### Profit Margin (Mar)
- **Definition**: The percentage of revenue remaining after accounting for the COGS.
- **Calculation**: 
  
  ```
  ((Revenue − Cost) / Revenue) ∗ 100
  ```

- **Data Sources**:
  - `transactionsanditems` table
  - `product_costs` table

- **Query Outline**:
  1. Join `transactionsanditems` with `product_costs` using `item_id`.
  2. Calculate total revenue and total cost for the given time period (1st January 2020 - 31st December 2021).
  3. Compute the profit margin percentage using the formula.

---

### Revenue (Shravya)
- **Definition**: The total revenue generated during a given month.
- **Calculation**:

  ```
  Total Revenue = ∑(transaction_total)
  ```

- **Data Sources**:
  - `Transaction` table

- **Query Outline**:
  1. Use the `transactions` table to access transaction details.
  2. Extract the month and year from the date field using `DATE_TRUNC(t.date, MONTH)` to group revenue data by month.
  3. Aggregate the `transaction_total` field to calculate total revenue for each month.

---

### Return on Ad Spend (Mar)
- **Definition**: The revenue generated for each £ spent on advertising.
- **Calculation**:

  ```
  Revenue / AdSpend
  ```

- **Data Sources**:
  - `transactionsanditems` table
  - `adplatform_data` table

- **Query Overview**:
  1. Aggregate the total revenue by month.
  2. Divide total revenue by ad spend/cost for each platform (Google and Meta).
  3. Handle cases where ad spend is zero to avoid division errors.

---

### Conversion Rate (Harini)
- **Definition**: The rate at which the number of visits turn into a fully completed purchase.
- **Calculation**:

  ```
  # of purchases / # of visits
  ```

- **Data Sources**:
  - `funnelevents` table

- **Query Overview**:
  1. Identify distinct visits per session that led to a purchase.
  2. Format and extract date by `month_year`.
  3. Group by `month_year` in ascending order.

---

### Retention Rate (Harini)
- **Definition**: The number of distinct users that have logged in since registering with Prism.
- **Calculation**:

  ```
  (# last_login_date > registration_date) / # user_id
  ```

- **Data Sources**:
  - `users` table

- **Query Overview**:
  1. Calculate the total number of users that have logged in at least once.
  2. Count the total number of registered users (`user_id`).
  3. Group by `month_year` in ascending order.

---

### Refund Rate (Mar)
- **Definition**: The percentage of transactions that resulted in a refund.
- **Calculation**:

  ```
  (Count of Refunds / Total Transactions) ∗ 100
  ```

- **Data Sources**:
  - `transactionsanditems` table
  - `product_returns` table

- **Query Overview**:
  1. Left join `transactionsanditems` with `product_returns` on `transaction_id`.
  2. Count refunded transactions (`COUNTIF`) and total transactions for the time period.
  3. Calculate the percentage of refunds.
  4. Ensure `return_status = 'Refund'`.

---

### User Sign Ups (Shravya)
- **Definition**: The percentage of website visitors or users who sign up for a specific action or service.
- **Calculation**:

  ```
  Sign-up Rate (%) = (Total Signups / Total Sessions) x 100
  ```

- **Data Sources**:
  - `Transactions` table
  - `Session` table

- **Query Overview**:
  1. Join `transactions` and `sessions` tables using the `user_crm_id` field to link users’ transactions and session data.
  2. Extract the month and year from the date field in the `transactions` table.
  3. Aggregate data to calculate:
     - Total Signups: Count distinct `user_crm`.

---
