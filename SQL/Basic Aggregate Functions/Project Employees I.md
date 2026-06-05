-- 【题目】✅1075. Project Employees I(Easy)
-- 【链接】https://leetcode.com/problems/project-employees-i/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT p.project_id,
        ROUND(AVG(e.experience_years),2) AS average_years 
FROM Project p
LEFT JOIN Employee e
ON p.employee_id=e.employee_id
GROUP BY p.project_id
```
