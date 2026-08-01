# 022. Game Play Analysis IV

## Problem

Find the fraction of players who logged in again on the day immediately after their first login.

Round the result to `2` decimal places.

## Table Schema

### Activity

| Column Name | Type |
| ----------- | ---- |
| player_id | int |
| device_id | int |
| event_date | date |
| games_played | int |

## Explanation

Use a subquery to find the first `event_date` for each player.

Join the result with the `Activity` table and check whether the player logged in again exactly one day after their first login using `DATE_ADD()`.

Count the number of such players and divide it by the total number of distinct players. Finally, round the result to `2` decimal places.

## SQL Concepts

- `SELECT`
- `JOIN`
- `Subquery`
- `MIN`
- `GROUP BY`
- `COUNT`
- `COUNT(DISTINCT)`
- `DATE_ADD`
- `ROUND`
- `AS`

## Solution

```sql
SELECT ROUND(COUNT(a.player_id) / (SELECT COUNT(DISTINCT player_id) FROM Activity),2) AS fraction
FROM Activity a
JOIN (
    SELECT player_id,MIN(event_date) AS login_date
    FROM Activity
    GROUP BY player_id
) d
ON a.player_id = d.player_id
WHERE a.event_date = DATE_ADD(d.login_date, INTERVAL 1 DAY);
```
