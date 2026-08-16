# 036. Count Salary Categories

## Problem

Calculate the number of bank accounts in each salary category.

The salary categories are:

- `"Low Salary"`: Income strictly less than `20000`.
- `"Average Salary"`: Income between `20000` and `50000`, inclusive.
- `"High Salary"`: Income strictly greater than `50000`.

All three categories must be included in the result, even if a category has `0` accounts.

## Table Schema

### Accounts

| Column Name | Type |
| ----------- | ---- |
| `account_id` | int |
| `income` | int |

## Explanation

Use separate `SELECT` statements to count the accounts belonging to each salary category.

Use `UNION ALL` to combine the three results into one table.

This approach ensures that all three salary categories are returned, even when there are no accounts in a particular category.

## SQL Concepts

- `SELECT`
- `CASE`
- `SUM`
- `UNION ALL`
- Comparison Operators

## Solution

```sql
SELECT 'Low Salary' AS category,
       SUM(income < 20000) AS accounts_count
FROM Accounts

UNION ALL

SELECT 'Average Salary',
       SUM(income BETWEEN 20000 AND 50000)
FROM Accounts

UNION ALL

SELECT 'High Salary',
       SUM(income > 50000)
FROM Accounts;
```
