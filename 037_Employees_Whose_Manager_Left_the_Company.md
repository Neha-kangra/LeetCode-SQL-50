# 037. Employees Whose Manager Left the Company

## Problem

Find the IDs of employees whose salary is strictly less than `30000` and whose manager has left the company.

When a manager leaves the company, their row is deleted from the `Employees` table, but the employee's `manager_id` remains unchanged.

## Table Schema

### Employees

| Column Name | Type |
| ----------- | ---- |
| `employee_id` | int |
| `name` | varchar |
| `manager_id` | int |
| `salary` | int |

## Explanation

Use a `LEFT JOIN` to match each employee with their manager.

If the manager has left the company, there will be no matching row in the `Employees` table, so `e2.employee_id` will be `NULL`.

Filter employees whose salary is less than `30000`, whose `manager_id` is not `NULL`, and whose manager does not exist in the table.

Finally, order the result by `employee_id`.

## SQL Concepts

- `SELECT`
- `LEFT JOIN`
- `IS NULL`
- `IS NOT NULL`
- `WHERE`
- `AND`
- `ORDER BY`
- Self Join

## Solution

```sql
SELECT e1.employee_id
FROM Employees e1
LEFT JOIN Employees e2
ON e1.manager_id = e2.employee_id
WHERE e1.salary < 30000
  AND e2.employee_id IS NULL
  AND e1.manager_id IS NOT NULL
ORDER BY employee_id;
```
