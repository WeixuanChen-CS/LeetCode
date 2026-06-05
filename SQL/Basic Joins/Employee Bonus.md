-- 【题目】✅577. Employee Bonus(Easy)
-- 【链接】https://leetcode.com/problems/employee-bonus/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT name,bonus
FROM Employee
LEFT Join Bonus
ON Employee.empId=Bonus.empId
WHERE bonus is null
OR bonus < 1000
```

==========================================
Conclusion
==========================================
```text
这里不是普通join，普通join会过滤掉没有bonus的员工
```