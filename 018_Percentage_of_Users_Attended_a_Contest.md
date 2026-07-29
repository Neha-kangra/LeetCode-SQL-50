# 018. Percentage of Users Attended a Contest

## Problem

Find the percentage of users registered in each contest.

Return the percentage rounded to `2` decimal places, ordered by `percentage` in descending order. If two contests have the same percentage, order them by `contest_id` in ascending order.

## Table Schema

### Users

| Column Name | Type |
| ----------- | ---- |
| user_id | int |
| user_name | varchar |

### Register

| Column Name | Type |
| ----------- | ---- |
| contest_id | int |
| user_id | int |

## Explanation

Use an `INNER JOIN` to match registered users with the `Users` table.

Count the number of users registered for each contest and divide it by the total number of users using a subquery.

Multiply the result by `100`, round it to `2` decimal places using `ROUND()`, then order the results by `percentage` in descending order and `contest_id` in ascending order.

## SQL Concepts

- `SELECT`
- `INNER JOIN`
- `ON`
- `COUNT`
- `ROUND`
- `Subquery`
- `GROUP BY`
- `ORDER BY`
- `AS`

## Solution

```sql
SELECT r.contest_id, ROUND( (COUNT(r.user_id) / (SELECT COUNT(*) FROM Users)) * 100, 2 ) AS percentage
FROM Users u JOIN Register r
ON u.user_id = r.user_id
GROUP BY r.contest_id
ORDER BY percentage DESC, r.contest_id ASC;
```
