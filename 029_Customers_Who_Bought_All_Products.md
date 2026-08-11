# 029. Customers Who Bought All Products

## Problem

Find the customers who bought every product listed in the `Product` table.

Return the result table in any order.

## Table Schema

### Customer

| Column Name | Type |
| ----------- | ---- |
| customer_id | int |
| product_key | int |

### Product

| Column Name | Type |
| ----------- | ---- |
| product_key | int |

## Explanation

Group the records by `customer_id`.

Use `COUNT(DISTINCT product_key)` to count the unique products purchased by each customer.

Compare this count with the total number of products in the `Product` table. If both counts are equal, the customer has bought all products.

## SQL Concepts

- `SELECT`
- `GROUP BY`
- `HAVING`
- `COUNT(DISTINCT)`
- `Subquery`

## Solution

```sql
SELECT customer_id
FROM Customer
GROUP BY customer_id
HAVING COUNT(DISTINCT product_key) = (SELECT COUNT(*) FROM Product);
```
