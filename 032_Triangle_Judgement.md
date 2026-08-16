# 032. Triangle Judgement

## Problem

Report for every three line segments whether they can form a triangle.

A triangle can be formed only if the sum of the lengths of any two sides is greater than the third side.

## Table Schema

### Triangle

| Column Name | Type |
| ----------- | ---- |
| `x` | int |
| `y` | int |
| `z` | int |

## Explanation

Check the triangle inequality theorem for each row.

A valid triangle must satisfy all three conditions:

- `x < y + z`
- `y < x + z`
- `z < x + y`

Use a `CASE` statement to return `"Yes"` if all conditions are true; otherwise return `"No"`.

## SQL Concepts

- `SELECT`
- `CASE`
- `WHEN`
- `AND`
- `AS`

## Solution

```sql
SELECT x, y, z, CASE WHEN x < y + z AND y < x + z AND z < x + y THEN "Yes" ELSE "No" END AS triangle
FROM Triangle;
```
