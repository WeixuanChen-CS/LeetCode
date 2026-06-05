-- 【题目】❌1633. Percentage of Users Attended a Contest (Easy)
-- 【链接】https://leetcode.com/problems/percentage-of-users-attended-a-contest/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT r.contest_id,
        ROUND(count(r.user_id)/(SELECT count(*) FROM Users)*100%,2) AS percentage
FROM USERS u
LEFT JOIN Register r
ON u.user_id=r.user_id
GROUP BY r.contest_id
ORDER BY percentage DESC, r.contest_id ASC
```

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.100% 写法错了

2.这题不太需要从 Users LEFT JOIN Register


```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT r.contest_id,
        ROUND(count(r.user_id)/(SELECT count(*) FROM Users)*100,2) AS percentage
FROM Register r
GROUP BY r.contest_id
ORDER BY percentage DESC, r.contest_id ASC
```

==========================================
Conclusion
==========================================
```text

1.SQL 里不能这样写百分号。这里不是显示百分号，而是把比例乘以 100。
直接写：* 100

2.不需要看到有两张表就想着要join
这题完全不需要join

```