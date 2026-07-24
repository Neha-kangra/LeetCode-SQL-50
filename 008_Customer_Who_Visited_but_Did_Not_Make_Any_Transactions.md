# 008. Customer Who Visited but Did Not Make Any Transactions

## Problem

Find the `customer_id` of customers who visited the mall but did not make any transactions, along with the number of such visits.

## Table Schema

### Visits

| Column Name | Type |
| ----------- | ---- |
| visit_id | int |
| customer_id | int |

### Transactions

| Column Name | Type |
| ----------- | ---- |
| transaction_id | int |
| visit_id | int |
| amount | int |

## Explanation

Join the `Visits` and `Transactions` tables using `visit_id`.

Filter the rows where no matching transaction exists by checking if `transaction_id` is `NULL`.

Group the results by `customer_id` and count the number of visits without transactions.

## SQL Concepts

- `SELECT`
- `LEFT JOIN`
- `WHERE`
- `IS NULL`
- `GROUP BY`
- `COUNT`

## Solution

```sql
SELECT v.customer_id, COUNT(*) AS count_no_trans
FROM Visits v LEFT JOIN Transactions t
ON v.visit_id = t.visit_id
WHERE t.transaction_id IS NULL
GROUP BY v.customer_id;
```
