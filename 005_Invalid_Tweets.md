# 005. Invalid Tweets

## Problem

Find the IDs of tweets where the content length is strictly greater than 15 characters.

## Table Schema

### Tweets

| Column Name | Type    |
|-------------|---------|
| tweet_id    | int     |
| content     | varchar |

## Explanation

Select the `tweet_id` from the `Tweets` table where the length of `content` is greater than `15`.

## SQL Concepts

- SELECT
- WHERE
- LENGTH()

## Solution

```sql
SELECT tweet_id
FROM Tweets
WHERE LENGTH(content) > 15;
```
