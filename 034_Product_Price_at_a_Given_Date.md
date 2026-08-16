# 034. Product Price at a Given Date

## Problem

Find the price of every product on `2019-08-16`.

- If a product had one or more price changes on or before `2019-08-16`, return its latest price.
- If a product had no price changes before or on that date, its price is assumed to be `10`.

## Table Schema

### Products

| Column Name | Type |
| ----------- | ---- |
| `product_id` | int |
| `new_price` | int |
| `change_date` | date |

## Explanation

Filter all price changes that occurred on or before `2019-08-16`.

Use the `ROW_NUMBER()` window function to assign rank `1` to the latest price change for each product.

Retrieve all distinct products and `LEFT JOIN` them with the latest prices.

Use `COALESCE()` to return the latest price if available; otherwise return the default price of `10`.

## SQL Concepts

- `WITH (CTE)`
- `ROW_NUMBER()`
- `PARTITION BY`
- `ORDER BY`
- `LEFT JOIN`
- `COALESCE()`
- `DISTINCT`
- `WHERE`

## Solution

```sql
WITH latest_price AS (SELECT product_id, new_price, ROW_NUMBER() OVER (PARTITION BY product_id ORDER BY change_date DESC) AS rn
    FROM Products
    WHERE change_date <= '2019-08-16'
)
SELECT p.product_id,COALESCE(lp.new_price, 10) AS price
FROM (SELECT DISTINCT product_id FROM Products) p
LEFT JOIN latest_price lp
ON p.product_id = lp.product_id
AND lp.rn = 1;
```
