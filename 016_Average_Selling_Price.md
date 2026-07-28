# 016. Average Selling Price

## Problem

Find the average selling price for each product.

The `average_price` is calculated as the total selling price divided by the total number of units sold. If a product has no sold units, its `average_price` should be `0`.

Round the result to `2` decimal places.

## Table Schema

### Prices

| Column Name | Type |
| ----------- | ---- |
| product_id | int |
| start_date | date |
| end_date | date |
| price | int |

### UnitsSold

| Column Name | Type |
| ----------- | ---- |
| product_id | int |
| purchase_date | date |
| units | int |

## Explanation

Use a `LEFT JOIN` to match each product with its sold units based on `product_id`.

Use the `BETWEEN` operator to ensure that each sale falls within the correct price period.

Calculate the weighted average selling price using:

- `SUM(price * units)` for the total selling value.
- `SUM(units)` for the total units sold.

Use `IFNULL()` to return `0` for products with no sales, and `ROUND()` to round the result to `2` decimal places.

## SQL Concepts

- `SELECT`
- `LEFT JOIN`
- `ON`
- `BETWEEN`
- `SUM`
- `GROUP BY`
- `IFNULL`
- `ROUND`
- `AS`

## Solution

```sql
SELECT p.product_id,
    ROUND(IFNULL(SUM(p.price * u.units) / SUM(u.units), 0),2) AS average_price
FROM Prices p LEFT JOIN UnitsSold u
ON p.product_id = u.product_id
AND u.purchase_date BETWEEN p.start_date AND p.end_date
GROUP BY p.product_id;
```
