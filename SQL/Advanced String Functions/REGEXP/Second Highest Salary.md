-- 【题目】❌176. Second Highest Salary (Medium)
-- 【链接】https://leetcode.com/problems/second-highest-salary

```sql
-- ==========================================
-- Correct solution
-- ==========================================
select(
    select distinct salary 
    from Employee
    order by salary desc
    limit 1,1
)AS SecondHighestSalary 
```

==========================================
Conclusion
==========================================
```text

1.子查询放在 FROM 后面：它是一张表
子查询放在 SELECT 后面：它是一个值,如果没有相对应的值就会返回null

```