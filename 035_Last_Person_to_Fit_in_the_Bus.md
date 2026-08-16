# 035. Last Person to Fit in the Bus

## Problem

Find the `person_name` of the last person who can board the bus without exceeding the weight limit of `1000` kilograms.

People board the bus in the order specified by the `turn` column.

## Table Schema

### Queue

| Column Name | Type |
| ----------- | ---- |
| `person_id` | int |
| `person_name` | varchar |
| `weight` | int |
| `turn` | int |

## Explanation

Calculate the cumulative weight of passengers in boarding order using the `SUM()` window function.

Filter the people whose cumulative weight does not exceed `1000`.

Sort the remaining passengers by `turn` in descending order and return the first one, which represents the last person who can successfully board the bus.

## SQL Concepts

- `WITH (CTE)`
- `SUM()`
- `Window Function`
- `OVER`
- `ORDER BY`
- `WHERE`
- `LIMIT`

## Solution

```sql
WITH busqueue AS (
    SELECT person_id,person_name,turn,
    SUM(weight) OVER (ORDER BY turn) AS total_weight
    FROM Queue
)
SELECT person_name
FROM busqueue
WHERE total_weight <= 1000
ORDER BY turn DESC
LIMIT 1;
```
