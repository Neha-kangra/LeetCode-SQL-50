# 38. Exchange Seats

## Problem

Swap the seat ID of every two consecutive students. If the number of students is odd, the last student's seat remains unchanged.

Return the result ordered by `id` in ascending order.

## Table Schema

### Seat

| **Column Name** | **Type** |
| --------------- | -------- |
| `id`            | int      |
| `student`       | varchar  |

## Explanation

Use a `CASE` statement to determine the new seat ID.

For odd IDs, increase the ID by `1` to swap it with the next student.

For even IDs, decrease the ID by `1` to swap it with the previous student.

If the number of students is odd and the current `id` is the last ID, keep the ID unchanged.

Finally, order the result by `id`.

## SQL Concepts

* `SELECT`
* `CASE`
* `COUNT() OVER()`
* Window Functions
* Modulo Operator `%`
* `WHEN`
* `THEN`
* `ELSE`
* `ORDER BY`

## Solution

```sql
SELECT CASE
           WHEN id = COUNT(*) OVER () AND id % 2 = 1 THEN id
           WHEN id % 2 = 1 THEN id + 1
           WHEN id % 2 = 0 THEN id - 1
       END AS id,
       student
FROM Seat
ORDER BY id;
```
