# 012. Students and Examinations

## Problem

Find the number of times each student attended each subject examination.

Return the result ordered by `student_id` and `subject_name`.

## Table Schema

### Students

| Column Name | Type |
| ----------- | ---- |
| student_id | int |
| student_name | varchar |

### Subjects

| Column Name | Type |
| ----------- | ---- |
| subject_name | varchar |

### Examinations

| Column Name | Type |
| ----------- | ---- |
| student_id | int |
| subject_name | varchar |

## Explanation

Use a `CROSS JOIN` to generate all possible combinations of students and subjects.

Then use a `LEFT JOIN` to match each student-subject combination with the `Examinations` table.

Count the number of matching examination records for each student and subject.

Finally, group the results by `student_id`, `student_name`, and `subject_name`, and sort them by `student_id` and `subject_name`.

## SQL Concepts

- `SELECT`
- `CROSS JOIN`
- `LEFT JOIN`
- `ON`
- `COUNT`
- `GROUP BY`
- `ORDER BY`

## Solution

```sql
SELECT s.student_id,s.student_name,su.subject_name,COUNT(e.student_id) AS attended_exams
FROM Students s
CROSS JOIN Subjects su
LEFT JOIN Examinations e
ON s.student_id = e.student_id
AND su.subject_name = e.subject_name
GROUP BY s.student_id,s.student_name,su.subject_name
ORDER BY s.student_id,su.subject_name;
```
