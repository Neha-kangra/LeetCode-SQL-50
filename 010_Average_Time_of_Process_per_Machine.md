# 010. Average Time of Process per Machine

## Problem

Find the average time each machine takes to complete a process.

The processing time for a process is calculated as the difference between the `end` timestamp and the `start` timestamp. Return the average processing time for each `machine_id`, rounded to `3` decimal places.

## Table Schema

### Activity

| Column Name | Type |
| ----------- | ---- |
| machine_id | int |
| process_id | int |
| activity_type | enum |
| timestamp | float |

## Explanation

Use a `SELF JOIN` on the `Activity` table to match the `start` and `end` records for the same `machine_id` and `process_id`.

Calculate the processing time for each process by subtracting the `start` timestamp from the `end` timestamp.

Group the results by `machine_id`, calculate the average processing time using `AVG()`, and round the result to `3` decimal places using `ROUND()`.

## SQL Concepts

- `SELECT`
- `SELF JOIN`
- `ON`
- `WHERE`
- `AVG`
- `GROUP BY`
- `ROUND`
- `AS`

## Solution

```sql
SELECT
    a.machine_id,
    ROUND(AVG(b.timestamp - a.timestamp), 3) AS processing_time
FROM Activity a
JOIN Activity b
ON a.machine_id = b.machine_id
AND a.process_id = b.process_id
WHERE a.activity_type = 'start'
AND b.activity_type = 'end'
GROUP BY a.machine_id;
```
