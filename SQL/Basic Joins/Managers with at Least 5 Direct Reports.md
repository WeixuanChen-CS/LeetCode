-- 【题目】❌570. Managers with at Least 5 Direct Reports (Medium)
-- 【链接】https://leetcode.com/problems/managers-with-at-least-5-direct-reports/

```sql
-- ==========================================
-- My solution
-- ==========================================
# Write your MySQL query statement below
SELECT m.name AS name
FROM Employee e
JOIN Employee m
ON m.managerId=e.id
GROUP BY m.id,m.name
HAVING count(*)>=5
```

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.自连接理解不到位，自连接用错ON

2.不知道having的用法

3.两张表的id指向弄混

```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT m.name AS name
FROM Employee e
JOIN Employee m
ON e.managerId=m.id
GROUP BY m.id,m.name
HAVING count(*)>=5
```

==========================================
Conclusion
==========================================
```text

1.WHERE  是分组前筛选行, HAVING 是分组后筛选组

2.对JOIN的理解：
拿左表的一行
去右表里找满足 ON 条件的行
找到后，把两行横向拼起来
找不到时：
  INNER JOIN：这行不要
  LEFT JOIN：保留左边，右边补 NULL

3.当你需要先算出一个中间结果，再基于这个中间结果继续筛选、统计、排序时，就可能需要子表。
如果一层查询已经能直接完成，就不要强行套子表

```