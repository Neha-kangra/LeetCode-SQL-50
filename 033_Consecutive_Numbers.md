# 033. Consecutive Numbers

## Problem

Find all numbers that appear at least three times consecutively.

Return each qualifying number only once.

## Table Schema

### Logs

| Column Name | Type |
| ----------- | ---- |
| `id` | int |
| `num` | varchar |

## Explanation

Use the `LEAD()` window function to compare each number with the next two numbers based on `id`.

If the current value is equal to both the next value and the value after that, then it appears at least three times consecutively.

Use `DISTINCT` to ensure each qualifying number appears only once in the result.

## SQL Concepts

- `SELECT`
- `DISTINCT`
- `LEAD()`
- `Window Function`
- `OVER`
- `ORDER BY`
- `Subquery`
- `WHERE`
- `AS`

## Solution

```sql
SELECT DISTINCT num AS ConsecutiveNums
FROM (SELECT
        num,
        LEAD(num, 1) OVER (ORDER BY id) AS next1,
        LEAD(num, 2) OVER (ORDER BY id) AS next2
      FROM Logs
) N
WHERE num = next1
  AND num = next2;
```
