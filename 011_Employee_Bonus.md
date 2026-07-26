# 011. Employee Bonus

## Problem

Report the `name` and `bonus` of each employee who:

- has a `bonus` less than `1000`, or
- did not receive any bonus.

## Table Schema

### Employee

| Column Name | Type |
| ----------- | ---- |
| empId | int |
| name | varchar |
| supervisor | int |
| salary | int |

### Bonus

| Column Name | Type |
| ----------- | ---- |
| empId | int |
| bonus | int |

## Explanation

Use a `LEFT JOIN` to combine the `Employee` and `Bonus` tables using `empId`.

Return employees whose `bonus` is less than `1000` or whose `bonus` is `NULL`, indicating they did not receive a bonus.

## SQL Concepts

- `SELECT`
- `LEFT JOIN`
- `ON`
- `WHERE`
- `OR`
- `IS NULL`

## Solution

```sql
SELECT e.name, b.bonus
FROM Employee e
LEFT JOIN Bonus b
ON e.empId = b.empId
WHERE b.bonus < 1000
   OR b.bonus IS NULL;
```
