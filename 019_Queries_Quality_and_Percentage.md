# 019. Queries Quality and Percentage

## Problem

Find the `quality` and `poor_query_percentage` for each `query_name`.

- `quality` is the average of `rating / position`.
- `poor_query_percentage` is the percentage of queries with a `rating` less than `3`.

Round both values to `2` decimal places.

## Table Schema

### Queries

| Column Name | Type |
| ----------- | ---- |
| query_name | varchar |
| result | varchar |
| position | int |
| rating | int |

## Explanation

Group the records by `query_name`.

Calculate the average query quality using `AVG(rating / position)`.

Use a `CASE` expression to identify poor queries (`rating < 3`), calculate their average, multiply by `100` to get the percentage, and round both results to `2` decimal places.

## SQL Concepts

- `SELECT`
- `AVG`
- `CASE`
- `ROUND`
- `GROUP BY`
- `AS`

## Solution

```sql
SELECT query_name, ROUND(AVG(rating / position), 2) AS quality,
    ROUND(AVG(CASE WHEN rating < 3 THEN 1 ELSE 0 END) * 100, 2) AS poor_query_percentage
FROM Queries
GROUP BY query_name;
```
