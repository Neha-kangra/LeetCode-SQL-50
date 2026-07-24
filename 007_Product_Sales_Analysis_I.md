# 005. Product Sales Analysis I

## Problem

Report the `product_name`, `year`, and `price` for each sale in the `Sales` table.

## Table Schema

### Sales

| Column Name | Type |
| ----------- | ---- |
| sale_id     | int  |
| product_id  | int  |
| year        | int  |
| quantity    | int  |
| price       | int  |

### Product

| Column Name | Type |
| ----------- | ---- |
| product_id  | int  |
| product_name| varchar |

## Explanation

Join the `Sales` and `Product` tables using `product_id`.

Select the following columns:

- `product_name` from the `Product` table
- `year` from the `Sales` table
- `price` from the `Sales` table

## SQL Concepts

- `SELECT`
- `JOIN`
- `ON`

## Solution

```sql
SELECT p.product_name, s.year, s.price
FROM Sales s LEFT JOIN Product p
ON s.product_id = p.product_id;
```
