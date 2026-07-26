# 009. Rising Temperature

## Problem

Find the `id` of all dates where the temperature is higher than the previous day's temperature.

## Table Schema

### Weather

| Column Name | Type |
| ----------- | ---- |
| id | int |
| recordDate | date |
| temperature | int |

## Explanation

Use a `SELF JOIN` on the `Weather` table to compare each day's temperature with the previous day's temperature.

Match records where the difference between the two `recordDate` values is exactly one day, then return the `id` of the day whose `temperature` is higher than the previous day's temperature.

## SQL Concepts

- `SELECT`
- `SELF JOIN`
- `ON`
- `DATEDIFF`
- `WHERE`

## Solution

```sql
SELECT w1.id
FROM Weather w1
JOIN Weather w2
ON DATEDIFF(w1.recordDate, w2.recordDate) = 1
WHERE w1.temperature > w2.temperature;
```
