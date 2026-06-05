-- 【题目】❌1280. Students and Examinations (Easy)
-- 【链接】https://leetcode.com/problems/students-and-examinations/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT s.user_id, 
        round(sum(c.action='confirmed')/count(c.action),2) AS confirmation_rate
FROM Signups s
LEFT JOIN Confirmations c
ON s.user_id=c.user_id
GROUP BY s.user_id
```

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.没有理解题目的rate到底是什么。这里的rate：
confirmed/confirmed+timeout

2.对于action是null的，要用0代替，这里用到
IFNULL(表达式, 替代值)
如果表达式是 NULL，就返回替代值；
如果表达式不是 NULL，就返回表达式本身。

```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT s.user_id, 
        round(IFNULL((sum(c.action='confirmed')/count(c.action)),0),2) AS confirmation_rate
FROM Signups s
LEFT JOIN Confirmations c
ON s.user_id=c.user_id
GROUP BY s.user_id
```

==========================================
Conclusion
==========================================
```text

1.SELECT里可以做很长的计算

2.这个题也可以直接用AVG算更简单

```