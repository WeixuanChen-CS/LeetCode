-- 【题目】✅1731. The Number of Employees Which Report to Each Employee(Easy)
-- 【链接】https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT m.employee_id,
        m.name,
        count(m.employee_id) AS reports_count,
        ROUND(AVG(e.age)) AS average_age 
FROM Employees e
JOIN Employees m
ON e.reports_to=m.employee_id
GROUP BY m.employee_id
ORDER BY m.employee_id

```
