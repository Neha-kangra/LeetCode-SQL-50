# 027. Find Followers Count

## Problem

Find the number of followers for each user.

Return the result ordered by `user_id` in ascending order.

## Table Schema

### Followers

| Column Name | Type |
| ----------- | ---- |
| user_id | int |
| follower_id | int |

## Explanation

Group the records by `user_id`.

Use `COUNT()` to calculate the number of followers for each user and sort the result by `user_id` in ascending order.

## SQL Concepts

- `SELECT`
- `COUNT`
- `GROUP BY`
- `ORDER BY`
- `AS`

## Solution

```sql
SELECT user_id,COUNT(follower_id) AS followers_count
FROM Followers
GROUP BY user_id
ORDER BY user_id;
```
