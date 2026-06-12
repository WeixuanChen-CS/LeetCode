-- 【题目】✅610. Triangle Judgement(Easy)
-- 【链接】https://leetcode.com/problems/triangle-judgement

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT x,y,z,
    IF(
        x+y>z AND x+z>y AND y+z>x,'Yes','No'
        ) AS triangle
FROM Triangle
```

==========================================
Conclusion
==========================================
```text
1.三角形成立条件两边之和大于第三边要比三次

2.IF(条件, 条件成立时返回的值, 条件不成立时返回的值)
也就是：
IF(condition, value_if_true, value_if_false)
```