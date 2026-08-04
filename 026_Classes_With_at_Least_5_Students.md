# 026. Classes With at Least 5 Students

## Problem

Find all classes that have at least five students enrolled.

Return the result table in any order.

## Table Schema

### Courses

| Column Name | Type |
| ----------- | ---- |
| student | varchar |
| class | varchar |

## Explanation

Group the records by `class`.

Use `COUNT()` to count the number of students in each class and return only those classes with at least `5` students.

## SQL Concepts

- `SELECT`
- `GROUP BY`
- `HAVING`
- `COUNT`

## Solution

```sql
SELECT class
FROM Courses
GROUP BY class
HAVING COUNT(*) >= 5;
```
