-- 【题目】❌1141. User Activity for the Past 30 Days I (Medium)
-- 【链接】https://leetcode.com/problems/user-activity-for-the-past-30-days-i/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT product_id,
        MIN(year) AS first_year,
        quantity,price
FROM Sales
GROUP BY product_id
```

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.GROUP BY product_id 之后，每个 product_id 只剩一组。
MIN(year) 可以确定是最早年份，但 quantity 和 price 没有聚合，也没有说明要取哪一行的值。
所以 MySQL 可能“随便拿这一组里的某一行”的 quantity 和 price。

2.题目要求的是：
如果一个产品在第一年有多条 sale，都要返回

```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT 
    product_id,
    year AS first_year,
    quantity,
    price
FROM Sales
WHERE (product_id, year) IN (
    SELECT 
        product_id,
        MIN(year)
    FROM Sales
    GROUP BY product_id
)
```

==========================================
Conclusion
==========================================
```text

1.这个思路就是：
我不仅要找到最小的一年，我还要那一年的所有信息，如果我只是在select里用min对year做处理，不处理其他的东西，其他的列sql就会随便选。
相反，我需要做的是找出一个中间表，这个中间表包含每个id在min（year）的相对应的所有信息，然后再从这个中间表里找题目需要的列

```

