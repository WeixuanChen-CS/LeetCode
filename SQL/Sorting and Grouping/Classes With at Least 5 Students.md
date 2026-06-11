-- 【题目】✅596. Classes With at Least 5 Students(Easy)
-- 【链接】https://leetcode.com/problems/classes-with-at-least-5-students/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT class
FROM Courses
GROUP BY class
HAVING COUNT(student)>=5
```

==========================================
Conclusion
==========================================
```text
WHERE 里不能直接用 SUM() / COUNT() 这种聚合函数。
因为 SQL 执行顺序大概是：
FROM
WHERE        -- 先筛原始行
GROUP BY     -- 再分组
HAVING       -- 分组后筛选
SELECT
所以在 WHERE 的时候，还没有 GROUP BY，也就还没有 SUM() / COUNT()。
```