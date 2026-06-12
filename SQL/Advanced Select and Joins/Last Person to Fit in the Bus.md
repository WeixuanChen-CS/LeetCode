-- 【题目】❌1204. Last Person to Fit in the Bus (Medium)
-- 【链接】https://leetcode.com/problems/last-person-to-fit-in-the-bus/

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT person_name
FROM(
    SELECT person_name,turn,
    SUM(weight) Over (Order By turn) AS total_weight
    FROM Queue)q
WHERE q.total_weight<=1000
ORDER BY q.turn DESC
LIMIT 1
```

==========================================
Conclusion
==========================================
```text

1.要用到窗口函数，因为涉及到累加和但是不需要分组
2.中间表就是按turn从小到大排列，然后算累加和，但是最后结果只要一个名字，且是最后一个能上车的人的名字
所以要把整个表倒序，然后只取第一行


```
