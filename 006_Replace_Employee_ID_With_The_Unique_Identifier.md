# 006. Replace Employee ID With The Unique Identifier

## Problem

Show the `unique_id` of each employee. If an employee does not have a unique ID, display `NULL`.

## Table Schema

### Employees

| Column Name | Type    |   
|-------------|---------|
| id          | int     |
| name        | varchar |

### EmployeeUNI

| Column Name | Type |
|-------------|------|
| id          | int  |
| unique_id   | int  |

## Explanation

Retrieve the `unique_id` and `name` for every employee. If an employee does not have a matching record in the `EmployeeUNI` table, display `NULL` for the `unique_id`.

## SQL Concepts

- SELECT
- RIGHT JOIN
- NULL

## Solution

```sql
SELECT eu.unique_id, e.name
FROM EmployeeUNI eu
RIGHT JOIN Employees e
ON eu.id = e.id;
```
