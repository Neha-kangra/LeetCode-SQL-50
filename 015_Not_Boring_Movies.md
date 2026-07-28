# 015. Not Boring Movies

## Problem

Find all movies that:

- Have an odd-numbered `id`.
- Have a `description` that is not `'boring'`.

Return the result ordered by `rating` in descending order.

## Table Schema

### Cinema

| Column Name | Type |
| ----------- | ---- |
| id | int |
| movie | varchar |
| description | varchar |
| rating | float |

## Explanation

Select all columns from the `Cinema` table.

Filter the records to include only movies with an odd-numbered `id` and a `description` other than `'boring'`.

Finally, sort the results by `rating` in descending order.

## SQL Concepts

- `SELECT`
- `WHERE`
- `AND`
- `ORDER BY`
- Arithmetic Operator (`%`)

## Solution

```sql
SELECT id, movie, description, rating
FROM Cinema
WHERE (id % 2 != 0) AND (description != 'boring')
ORDER BY rating DESC;
```
