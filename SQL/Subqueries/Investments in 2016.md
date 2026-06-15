-- 【题目】❌585. Investments in 2016 (Medium)
-- 【链接】https://leetcode.com/problems/investments-in-2016

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT Round(sum(tiv_2016),2) AS tiv_2016
FROM Insurance
WHERE tiv_2015 in (
    SELECT tiv_2015
    FROM Insurance 
    GROUP BY tiv_2015
    HAVING count(*)>1)
AND (lat,lon) in(
    SELECT lat,lon
    FROM Insurance
    GROUP BY lat,lon
    HAVING count(*)=1)
```

==========================================
Conclusion
==========================================
```text

1.这道题思路：
条件 1：某列值重复
=> GROUP BY 这列 HAVING COUNT(*) > 1
条件 2：某组坐标唯一
=> GROUP BY lat, lon HAVING COUNT(*) = 1
最后回原表 WHERE 同时筛两个条件

2.要判断 一组列组合 (lat, lon) 是否在子查询结果里，必须给它们加括号
也就是(lat, lon) IN (...)
而不是lat, lon IN (...)

3.SQL 的 GROUP BY 支持多列分组，语法就是用逗号隔开：
GROUP BY 列1, 列2, 列3
它会自动把 (列1,列2,列3) 当成组合分组条件

```