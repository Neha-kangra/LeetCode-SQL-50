# 031. Primary Department for Each Employee

## Problem

Report all employees with their primary department.

- If an employee belongs to multiple departments, return the department where `primary_flag = 'Y'`.
- If an employee belongs to only one department, return that department even if `primary_flag = 'N'`.

## Table Schema

### Employee

| Column Name | Type |
| ----------- | ---- |
| `employee_id` | int |
| `department_id` | int |
| `primary_flag` | varchar |

## Explanation

Select employees whose `primary_flag` is `'Y'`.

Also find employees who belong to only one department using `GROUP BY` and `HAVING COUNT(*) = 1`.

Combine both conditions with `OR` to return the correct department for every employee.

## SQL Concepts

- `SELECT`
- `WHERE`
- `OR`
- `IN`
- `Subquery`
- `GROUP BY`
- `HAVING`

## Solution

```sql
SELECT employee_id, department_id
FROM Employee
WHERE primary_flag = 'Y' OR employee_id IN (
       SELECT employee_id
       FROM Employee
       GROUP BY employee_id
       HAVING COUNT(*) = 1);
```
