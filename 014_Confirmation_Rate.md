# 014. Confirmation Rate

## Problem

Find the `confirmation_rate` for each user.

The confirmation rate is calculated as:

- Number of `confirmed` messages ÷ Total confirmation requests.
- If a user did not request any confirmation messages, the confirmation rate is `0`.

Round the result to `2` decimal places.

## Table Schema

### Signups

| Column Name | Type |
| ----------- | ---- |
| user_id | int |
| time_stamp | datetime |

### Confirmations

| Column Name | Type |
| ----------- | ---- |
| user_id | int |
| time_stamp | datetime |
| action | enum |

## Explanation

Use a `LEFT JOIN` to include all users from the `Signups` table, even those who have no confirmation requests.

The expression `action = 'confirmed'` evaluates to `1` for confirmed requests and `0` for timeout requests.

Use `AVG()` to calculate the confirmation rate for each user. If a user has no confirmation records, `AVG()` returns `NULL`, so use `IFNULL()` to replace it with `0`.

Finally, use `ROUND()` to round the confirmation rate to `2` decimal places.

## SQL Concepts

- `SELECT`
- `LEFT JOIN`
- `ON`
- `AVG`
- `IFNULL`
- `ROUND`
- `GROUP BY`
- `AS`

## Solution

```sql
SELECT s.user_id,ROUND(IFNULL(AVG(c.action = 'confirmed'),0),2) AS confirmation_rate
FROM Signups s LEFT JOIN Confirmations c
ON s.user_id = c.user_id
GROUP BY s.user_id;
```
