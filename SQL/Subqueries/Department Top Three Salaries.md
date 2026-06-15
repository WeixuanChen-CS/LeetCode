-- 【题目】❌185. Department Top Three Salaries (Medium)
-- 【链接】https://leetcode.com/problems/department-top-three-salaries

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT product_id
FROM low_fats, recyclable
WHERE Type = Y
```

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.比反了，题目要的是今天的温度比前一天高

2.题目要求的是：
previous dates / yesterday
所以更好的做法是用record date而不是id去做比较，
并且要限制上一行的日期是昨天，因为也有可能是前天

```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT Department,Employee,Salary
FROM(
    SELECT
        d.name AS Department,
        e.name AS Employee,
        e.salary AS Salary,
        DENSE_RANK() OVER (
        PARTITION BY departmentId 
        ORDER BY salary DESC
        )AS ranking
    FROM Employee e
    JOIN Department d
    ON e.departmentId=d.id
)t
WHERE ranking<=3
```

==========================================
Conclusion
==========================================
```text

1.窗口函数要作为一列放进查询结果里

2.几个排序的窗口函数
ROW_NUMBER()	不管并列，强行编号	    1, 2, 3, 4
RANK()	        并列同名次，但会跳号	1, 2, 2, 4
DENSE_RANK()	并列同名次，不跳号	    1, 2, 2, 3

3.整体思路：
JOIN Employee 和 Department，拿到部门名、员工名、工资
用 DENSE_RANK() 按部门分组，对工资排名
外层 WHERE ranking <= 3

```
