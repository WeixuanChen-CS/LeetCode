-- 【题目】❌1789. Primary Department for Each Employee (Easy)
-- 【链接】https://leetcode.com/problems/primary-department-for-each-employee/

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT employee_id,department_id
FROM Employee
WHERE Primary_flag='Y'
    OR employee_id IN(
    SELECT employee_id
    FROM Employee
    Group BY employee_id
    HAVING count(*)=1
)
```

==========================================
Conclusion
==========================================
```text

1.这道题的想法是，要么p-f是Y的，要么只有一个dpt的，所以WHERE有两个条件
把其中一个转成子查询

```