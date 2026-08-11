# 028. Biggest Single Number

## Problem

Find the largest number that appears exactly once in the `MyNumbers` table.

If no such number exists, return `NULL`.

## Table Schema

### MyNumbers

| Column Name | Type |
| ----------- | ---- |
| num | int |

## Explanation

Group the records by `num`.

Use `HAVING COUNT(*) = 1` to keep only the numbers that appear exactly once.

Finally, use `MAX()` to return the largest single number. If there are no single numbers, `MAX()` returns `NULL`.

## SQL Concepts

- `SELECT`
- `MAX`
- `GROUP BY`
- `HAVING`
- `COUNT`
- `Subquery`
- `AS`

## Solution

```sql
SELECT MAX(num) AS num
FROM (
    SELECT num
    FROM MyNumbers
    GROUP BY num
    HAVING COUNT(*) = 1
) t;
```
