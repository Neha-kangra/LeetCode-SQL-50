# 013. Managers with at Least 5 Direct Reports

## Problem

Find the `name` of managers who have at least `5` direct reports.

## Table Schema

### Employee

| Column Name | Type |
| ----------- | ---- |
| id | int |
| name | varchar |
| department | varchar |
| managerId | int |

## Explanation

Use a `SELF JOIN` on the `Employee` table to match each employee with their manager.

Group the records by the manager's `id` and `name`.

Count the number of employees reporting to each manager and return the managers whose direct report count is at least `5`.

## SQL Concepts

- `SELECT`
- `SELF JOIN`
- `ON`
- `GROUP BY`
- `HAVING`
- `COUNT`

## Solution

```sql
SELECT e2.name
FROM Employee e1 JOIN Employee e2
ON e1.managerId = e2.id
GROUP BY e2.id, e2.name
HAVING COUNT(e1.id) >= 5;
```
