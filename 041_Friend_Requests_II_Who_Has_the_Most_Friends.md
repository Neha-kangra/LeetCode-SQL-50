# 041. Friend Requests II: Who Has the Most Friends

## Problem

Find the person who has the most friends and return their `id` and the number of friends.

A person can be a friend by either sending a request that was accepted or accepting a request.

The test cases guarantee that only one person has the most friends.

## Table Schema

### RequestAccepted

| Column Name | Type |
| ----------- | ---- |
| `requester_id` | int |
| `accepter_id` | int |
| `accept_date` | date |

## Explanation

First, count the number of accepted requests for each `requester_id`.

Then, count the number of accepted requests for each `accepter_id`.

Use `UNION ALL` to combine both results because both sides represent friends.

Group the combined results by `id` and use `SUM()` to calculate the total number of friends for each person.

Finally, order the result by `num` in descending order and use `LIMIT 1` to return the person with the most friends.

## SQL Concepts

- `SELECT`
- `COUNT()`
- `SUM()`
- `GROUP BY`
- `UNION ALL`
- Subquery
- `ORDER BY`
- `LIMIT`
- `AS`

## Solution

```sql
SELECT id, SUM(friend_count) AS num
FROM
(
    SELECT id, friend_count
    FROM 
    (
        SELECT requester_id AS id, COUNT(*) AS friend_count
        FROM RequestAccepted
        GROUP BY requester_id
    ) AS t1

    UNION ALL

    SELECT id, friend_count
    FROM
    (
        SELECT accepter_id AS id, COUNT(*) AS friend_count
        FROM RequestAccepted
        GROUP BY accepter_id
    ) AS t2
) AS total
GROUP BY id
ORDER BY num DESC
LIMIT 1;
