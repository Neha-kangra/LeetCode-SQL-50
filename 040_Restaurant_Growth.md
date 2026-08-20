# 040. Restaurant Growth

## Problem

Compute the moving average of how much the customer paid in a seven days window (current day + 6 days before).

`average_amount` should be rounded to two decimal places.

Return the result ordered by `visited_on` in ascending order.

## Table Schema

### Customer

| **Column NameType** |         |
| ------------------- | ------- |
| `customer_id`       | int     |
| `name`              | varchar |
| `visited_on`        | date    |
| `amount`            | int     |

## Explanation

First, calculate the total amount for each day.

Use a window function to calculate the seven-day moving total.

Calculate the average by dividing the seven-day total by `7` and round it to two decimal places.

Finally, filter out the first six days and order the result by `visited_on`.

## SQL Concepts

* `SELECT`
* `SUM`
* `GROUP BY`
* Window Functions
* `ROWS BETWEEN`
* `ROUND`
* `DATE_ADD`
* `WHERE`
* `ORDER BY`
* Subqueries

## Solution

```sql
SELECT visited_on,amount,ROUND(amount / 7, 2) AS average_amount
FROM (
    SELECT visited_on,
        SUM(amount) OVER (
            ORDER BY visited_on
            ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
        ) AS amount
    FROM (
        SELECT
            visited_on,
            SUM(amount) AS amount
        FROM Customer
        GROUP BY visited_on
    ) AS daily
) AS t
WHERE visited_on >= (
    SELECT DATE_ADD(MIN(visited_on), INTERVAL 6 DAY)
    FROM Customer
)
ORDER BY visited_on;
```
