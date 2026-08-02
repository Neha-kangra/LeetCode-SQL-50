# 024. User Activity for the Past 30 Days I

## Problem

Find the number of active users for each day during the 30-day period ending on `2019-07-27` (inclusive).

A user is considered active if they performed at least one activity on that day.

## Table Schema

### Activity

| Column Name | Type |
| ----------- | ---- |
| user_id | int |
| session_id | int |
| activity_date | date |
| activity_type | enum |

## Explanation

Filter the records to include only activities between `2019-06-28` and `2019-07-27`.

Group the records by `activity_date` and count the number of distinct users for each day.

## SQL Concepts

- `SELECT`
- `WHERE`
- `BETWEEN`
- `COUNT(DISTINCT)`
- `GROUP BY`
- `AS`

## Solution

```sql
SELECT activity_date AS day,COUNT(DISTINCT user_id) AS active_users
FROM Activity
WHERE activity_date BETWEEN '2019-06-28' AND '2019-07-27'
GROUP BY activity_date;
```
