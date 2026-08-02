# 023. Number of Unique Subjects Taught by Each Teacher

## Problem

Find the number of unique subjects taught by each teacher.

Return the result table in any order.

## Table Schema

### Teacher

| Column Name | Type |
| ----------- | ---- |
| teacher_id | int |
| subject_id | int |
| dept_id | int |

## Explanation

Group the records by `teacher_id`.

Use `COUNT(DISTINCT subject_id)` to count only unique subjects taught by each teacher, even if the same subject is taught in multiple departments.

## SQL Concepts

- `SELECT`
- `COUNT(DISTINCT)`
- `GROUP BY`
- `AS`

## Solution

```sql
SELECT teacher_id,COUNT(DISTINCT subject_id) AS cnt
FROM Teacher
GROUP BY teacher_id;
```
