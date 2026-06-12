-- 【题目】❌1164. Product Price at a Given Date (Mediumy)
-- 【链接】https://leetcode.com/problems/product-price-at-a-given-date

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT product_id,
        IFNULL(max(new_price),10) AS price
FROM Products
where change_date < '2019-08-16'
GROUP BY product_id
```

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.WHERE 会把没有符合日期的 product 直接删掉

2.MAX(new_price) 不是“最近日期的价格”

```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT product_id
from Products
Where low_fats='Y'
AND recyclable='Y'
```

==========================================
Conclusion
==========================================
```text

1.这题正确思路是：
每个 product 默认价格是 10
如果它在 2019-08-16 及以前有改价记录
就取 <= 2019-08-16 的最近一次 change_date 对应的 new_price

2.以后遇到这种“复杂多子查询题”怎么想？
你就用这个模板：
最终要输出谁？先保留所有主体。
每个主体要找一个什么关键值？用 GROUP BY + MIN/MAX/COUNT。
如果还要这个关键值所在行的其他列，就回原表 JOIN。
如果没匹配到要默认值，就 LEFT JOIN + IFNULL。

```