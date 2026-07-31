# 021. Immediate Food Delivery II

## Problem

Find the percentage of customers whose first order was an immediate order.

An order is considered immediate if the `customer_pref_delivery_date` is the same as the `order_date`.

Round the result to `2` decimal places.

## Table Schema

### Delivery

| Column Name | Type |
| ----------- | ---- |
| delivery_id | int |
| customer_id | int |
| order_date | date |
| customer_pref_delivery_date | date |

## Explanation

Use a subquery to find the first `order_date` for each customer.

Join the result with the `Delivery` table to retrieve only the first order of every customer.

Use a `CASE` expression to identify immediate orders, calculate the average using `AVG()`, multiply by `100` to get the percentage, and round the result to `2` decimal places.

## SQL Concepts

- `SELECT`
- `JOIN`
- `Subquery`
- `MIN`
- `GROUP BY`
- `CASE`
- `AVG`
- `ROUND`
- `AS`

## Solution

```sql
SELECT
    ROUND(AVG(CASE WHEN d.order_date = d.customer_pref_delivery_date THEN 1 ELSE 0 END) * 100,2)
AS immediate_percentage
FROM Delivery d
JOIN (
    SELECT customer_id,MIN(order_date) AS first_order
    FROM Delivery
    GROUP BY customer_id
) t
ON d.customer_id = t.customer_id
AND d.order_date = t.first_order;
```
