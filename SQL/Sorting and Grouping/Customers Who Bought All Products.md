-- 【题目】❌1045. Customers Who Bought All Products (Medium)
-- 【链接】https://leetcode.com/problems/customers-who-bought-all-products/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT customer_id
FROM Customer c
JOIN Product p
ON c.product_key=p.product_key
GROUP BY customer_id
HAVING count(DISTINCT c.product_key)=count(SELECT (product_key) from Product)
```

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.Having语句没写出来

2.count语法用错

```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT customer_id
FROM Customer c
JOIN Product p
ON c.product_key=p.product_key
GROUP BY customer_id
HAVING count(DISTINCT c.product_key)=(SELECT count(product_key) from Product)
```

==========================================
Conclusion
==========================================
```text

1.这里拿的是每个用户买的产品数去跟原来的产品表的产品数比较，而不是join后的表，join后两个表的product_key是相同的

2.COUNT() 里面应该放的是列名、表达式、或者 *
但不能直接放：
SELECT product_key FROM Product
因为这个子查询会返回一张表/多行值，不是一个可以直接被 COUNT() 包住的单个表达式。

```