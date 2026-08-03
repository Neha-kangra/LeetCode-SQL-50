# 025. Product Sales Analysis III

## Problem

Find all sales that occurred in the first year each product was sold.

For each product, identify its earliest sale year and return all sales records from that year.

## Table Schema

### Sales

| Column Name | Type |
| ----------- | ---- |
| sale_id | int |
| product_id | int |
| year | int |
| quantity | int |
| price | int |

## Explanation

Use a subquery to find the earliest `year` for each `product_id`.

Join the result with the `Sales` table on both `product_id` and `year` to retrieve all sales that occurred in the product's first year.

## SQL Concepts

- `SELECT`
- `JOIN`
- `Subquery`
- `MIN`
- `GROUP BY`
- `AS`

## Solution

```sql
SELECT s.product_id,s1.first_year,s.quantity,s.price
FROM Sales s
JOIN (
    SELECT product_id,MIN(year) AS first_year
    FROM Sales
    GROUP BY product_id
) s1
ON s.product_id = s1.product_id
AND s.year = s1.first_year;
```
