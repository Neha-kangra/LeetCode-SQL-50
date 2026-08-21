# 042. Investments in 2016

## Problem

Find the sum of `tiv_2016` for policyholders who satisfy both conditions:

- Their `tiv_2015` value is shared by at least one other policyholder.
- Their `(lat, lon)` location is unique and is not shared by any other policyholder.

Round the final result to two decimal places.

## Table Schema

### Insurance

| Column Name | Type |
| ----------- | ---- |
| `pid` | int |
| `tiv_2015` | float |
| `tiv_2016` | float |
| `lat` | float |
| `lon` | float |

## Explanation

First, find all `tiv_2015` values that appear more than once using `GROUP BY` and `HAVING COUNT(*) > 1`.

Then, find all `(lat, lon)` pairs that appear exactly once using `GROUP BY` and `HAVING COUNT(*) = 1`.

Use these two conditions in the `WHERE` clause to select only the policyholders who satisfy both requirements.

Finally, use `SUM()` to calculate the total `tiv_2016` and `ROUND()` to round the result to two decimal places.

## SQL Concepts

- `SELECT`
- `SUM()`
- `ROUND()`
- `WHERE`
- `IN`
- `GROUP BY`
- `HAVING`
- Composite Columns
- Subquery
- `AS`

## Solution

```sql
SELECT ROUND(SUM(tiv_2016), 2) AS tiv_2016
FROM Insurance
WHERE tiv_2015 IN
(
    SELECT tiv_2015
    FROM Insurance
    GROUP BY tiv_2015
    HAVING COUNT(*) > 1
)
AND (lat, lon) IN
(
    SELECT lat, lon
    FROM Insurance
    GROUP BY lat, lon
    HAVING COUNT(*) = 1
);
