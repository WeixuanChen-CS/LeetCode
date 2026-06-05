-- 【题目】❌1251. Average Selling Price (Easy)
-- 【链接】https://leetcode.com/problems/average-selling-price/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT p.product_id,
        ROUND(avg(p.price*u.units) AS average_price,2)
FROM Prices p
LEFT JOIN UnitsSold u
ON p.product_id=u.product_id
GROUP BY p.product_id
```

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.这里要用 加权平均，不是普通平均
这是AVG的过程：
AVG(5*100, 10*15)
= AVG(500, 150)
= 325
但是这里要的不是这种普通平均，是加权平均

2.没限制没有unit的商品价格为0

3.JOIN的时候只用了id相等这一个条件，但是仔细看就会发现，同一个产品可能会和多个价格区间乱配，
所以还应该限制购买日期是在start和end之间

```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT p.product_id,
        IFNULL(ROUND(sum(p.price*u.units)/sum(u.units),2),0) AS average_price
FROM Prices p
LEFT JOIN UnitsSold u
ON p.product_id=u.product_id
AND u.purchase_date BETWEEN p.start_date AND p.end_date
GROUP BY p.product_id
```

