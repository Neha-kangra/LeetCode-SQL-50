# 002. Find Customer Referee

## Problem

Find the names of customers who are:
- Referred by any customer with `id != 2`, or
- Not referred by any customer.

## Table Schema

### Customer

| Column Name | Type |
|-------------|------|
| id          | int  |
| name        | varchar |
| referee_id  | int  |

## Explanation

Select the `name` from the `Customer` table where:
- `referee_id` is not equal to `2`, or
- `referee_id` is `NULL`.

## SQL Concepts

- SELECT
- WHERE
- OR
- IS NULL

## Solution

```sql
SELECT name
FROM Customer
WHERE referee_id != 2
   OR referee_id IS NULL;
```
