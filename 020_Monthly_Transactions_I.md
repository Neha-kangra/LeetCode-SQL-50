# 020. Monthly Transactions I

## Problem

For each month and country, find:

- The total number of transactions.
- The number of approved transactions.
- The total transaction amount.
- The total approved transaction amount.

## Table Schema

### Transactions

| Column Name | Type |
| ----------- | ---- |
| id | int |
| country | varchar |
| state | enum |
| amount | int |
| trans_date | date |

## Explanation

Use `DATE_FORMAT()` to extract the month from `trans_date` in the `YYYY-MM` format.

Group the records by `month` and `country`.

Use `COUNT()` to calculate the total number of transactions and `SUM()` to calculate the total transaction amount.

Use `CASE` expressions to count only approved transactions and sum the amounts of approved transactions.

## SQL Concepts

- `SELECT`
- `DATE_FORMAT`
- `COUNT`
- `SUM`
- `CASE`
- `GROUP BY`
- `AS`

## Solution

```sql
SELECT DATE_FORMAT(trans_date, '%Y-%m') AS month,
    country,
    COUNT(*) AS trans_count,
    SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END) AS approved_count,
    SUM(amount) AS trans_total_amount,
    SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END) AS approved_total_amount
FROM Transactions
GROUP BY DATE_FORMAT(trans_date, '%Y-%m'), country;
```
