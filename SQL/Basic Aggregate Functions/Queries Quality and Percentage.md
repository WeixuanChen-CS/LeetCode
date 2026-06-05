-- 【题目】✅1211. Queries Quality and Percentage(Easy)
-- 【链接】https://leetcode.com/problems/queries-quality-and-percentage/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT query_name,
        ROUND(AVG(rating/position),2) AS quality,
        ROUND(AVG(rating<3)*100,2) AS poor_query_percentage
FROM Queries
GROUP BY query_name
```

==========================================
Conclusion
==========================================
```text
要除以行数的可以先考虑AVG
你可以把 AVG(x) 翻译成：
先给每一行算出 x，然后把所有 x 加起来，再除以行数。
```