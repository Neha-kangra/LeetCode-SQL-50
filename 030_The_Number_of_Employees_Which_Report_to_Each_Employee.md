# 030. The Number of Employees Which Report to Each Employee

## Problem

Find all managers, the number of employees who report directly to them, and the average age of their direct reports.

Round the average age to the nearest integer and order the result by `employee_id`.

## Table Schema

### Employees

| Column Name | Type |
| ----------- | ---- |
| employee_id | int |
| name | varchar |
| reports_to | int |
| age | int |

## Explanation

Use a self-join on the `Employees` table to match each manager with their direct reports.

Group the results by the manager's `employee_id` and `name`.

Use `COUNT()` to find the number of direct reports and `AVG()` to calculate their average age. Use `ROUND()` to round the average age to the nearest integer.

## SQL Concepts

- `SELECT`
- `Self Join`
- `JOIN`
- `COUNT`
- `AVG`
- `ROUND`
- `GROUP BY`
- `ORDER BY`
- `AS`

## Solution

```sql
SELECT m.employee_id,m.name,COUNT(e.employee_id) AS reports_count,ROUND(AVG(e.age)) AS average_age
FROM Employees m JOIN Employees e
ON m.employee_id = e.reports_to
GROUP BY m.employee_id, m.name
ORDER BY m.employee_id;
```
