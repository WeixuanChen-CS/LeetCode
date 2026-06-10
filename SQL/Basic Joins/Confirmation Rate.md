-- 【题目】❌1934. Confirmation Rate (Medium)
-- 【链接】https://leetcode.com/problems/confirmation-rate/description/

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.不知道ifnull的用法

2.题目里比例的公式没搞清楚

```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT 
    s.user_id,
    ROUND(
        IFNULL(
            SUM(c.action = 'confirmed') / 
            (SUM(c.action = 'confirmed') + SUM(c.action = 'timeout')),
            0
        ),
        2
    ) AS confirmation_rate
FROM Signups s
LEFT JOIN Confirmations c
ON s.user_id = c.user_id
GROUP BY s.user_id;
```

==========================================
Conclusion
==========================================
```text

1.IFNULL 的作用是：
如果某个值是 NULL，就用另一个值替代它。
语法：IFNULL(字段或表达式, 替代值)
意思是：
如果第一个参数不是 NULL，就返回第一个参数；
如果第一个参数是 NULL，就返回第二个参数。

```