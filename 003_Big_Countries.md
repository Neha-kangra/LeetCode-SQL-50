# 003. Big Countries

## Problem
Find the name, population, and area of countries that are considered **big**.

A country is **big** if:
- Its area is at least **3,000,000 km²**, or
- Its population is at least **25,000,000**.

## Table Schema

### World

| Column Name | Type    |
|-------------|---------|
| name        | varchar |
| continent   | varchar |
| area        | int     |
| population  | int     |
| gdp         | bigint  |

## Explanation

Select the `name`, `population`, and `area` from the `World` table where either:

- `area >= 3000000`, or
- `population >= 25000000`

Since a country is considered big if `at least one` of these conditions is true, use the OR operator.

## SQL Concepts

- SELECT
- WHERE
- OR

## Solution

```sql
SELECT name, population, area
FROM World
WHERE area >= 3000000 OR population >= 25000000;
```
