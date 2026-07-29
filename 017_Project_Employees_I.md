# 017. Project Employees I

## Problem

Find the average experience years of all employees working on each project.

Return the average experience as `average_years`, rounded to `2` decimal places.

## Table Schema

### Project

| Column Name | Type |
| ----------- | ---- |
| project_id | int |
| employee_id | int |

### Employee

| Column Name | Type |
| ----------- | ---- |
| employee_id | int |
| name | varchar |
| experience_years | int |

## Explanation

Use an `INNER JOIN` to match each project with its employees using `employee_id`.

Calculate the average `experience_years` for each project using `AVG()`, round the result to `2` decimal places with `ROUND()`, and group the results by `project_id`.

## SQL Concepts

- `SELECT`
- `INNER JOIN`
- `ON`
- `AVG`
- `ROUND`
- `GROUP BY`
- `AS`

## Solution

```sql
SELECT p.project_id, ROUND(AVG(e.experience_years), 2) AS average_years
FROM Project p JOIN Employee e
ON p.employee_id = e.employee_id
GROUP BY p.project_id;
```
