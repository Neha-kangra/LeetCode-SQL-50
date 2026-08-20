# 039. Movie Rating

## Problem

Find the name of the user who has rated the greatest number of movies. In case of a tie, return the lexicographically smaller user name.

Also, find the movie name with the highest average rating in `February 2020`. In case of a tie, return the lexicographically smaller movie name.

## Table Schema

### Movies

| **Column NameType** |         |
| ------------------- | ------- |
| `movie_id`          | int     |
| `title`             | varchar |

### Users

| **Column NameType** |         |
| ------------------- | ------- |
| `user_id`           | int     |
| `name`              | varchar |

### MovieRating

| **Column NameType** |      |
| ------------------- | ---- |
| `movie_id`          | int  |
| `user_id`           | int  |
| `rating`            | int  |
| `created_at`        | date |

## Explanation

Use a `JOIN` between `MovieRating` and `Users` to count how many movies each user has rated.

Order the users by the number of ratings in descending order and by name in ascending order to handle ties. Select the user with the highest rating count.

For the second result, use a `JOIN` between `MovieRating` and `Movies` and filter the ratings to `February 2020`.

Calculate the average rating for each movie using `AVG()`. Order the movies by average rating in descending order and by title in ascending order to handle ties. Select the movie with the highest average rating.

Finally, combine both results using `UNION ALL`.

## SQL Concepts

* `SELECT`
* `JOIN`
* `COUNT`
* `AVG`
* `GROUP BY`
* `WHERE`
* `ORDER BY`
* `LIMIT`
* `UNION ALL`
* Subqueries
* Date Filtering

## Solution

```sql
SELECT name AS results
FROM
(
    SELECT COUNT(rating) AS rating_count, name
    FROM MovieRating mr
    JOIN Users u
    ON mr.user_id = u.user_id
    GROUP BY mr.user_id
    ORDER BY rating_count DESC, name ASC
    LIMIT 1
) AS t1

UNION ALL

SELECT title
FROM
(
    SELECT AVG(rating) AS average_rating, title
    FROM MovieRating mr
    JOIN Movies m
    ON mr.movie_id = m.movie_id
    WHERE created_at >= "2020-02-01"
      AND created_at < "2020-03-01"
    GROUP BY mr.movie_id
    ORDER BY average_rating DESC, title ASC
    LIMIT 1
) AS t2;
```
