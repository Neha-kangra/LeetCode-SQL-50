# 003. Article Views I

## Problem

Find all authors who viewed at least one of their own articles.

Return the result sorted by `id` in ascending order.

## Table Schema

### Views

| Column Name | Type |
| ----------- | ---- |
| article_id  | int  |
| author_id   | int  |
| viewer_id   | int  |
| view_date   | date |

## Explanation

Select the `author_id` (renamed as `id`) from the `Views` table where:

- `author_id` is equal to `viewer_id`.

Since the table may contain duplicate rows, use `DISTINCT` to return each author only once.

Sort the result by `id` in ascending order.

## SQL Concepts

- SELECT
- DISTINCT
- WHERE
- ORDER BY
- AS

## Solution

```sql
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY id;
```
