-- 【题目】❌1174. Immediate Food Delivery II (Medium)
-- 【链接】https://leetcode.com/problems/immediate-food-delivery-ii/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT round(sum(IF(t.order_date=t.customer_pref_delivery_date,1,0)/count(Delivery.*),2) AS immediate_percentage 
FROM(
    SELECT order_date,customer_pref_delivery_date 
    FROM Delivery
    GROUP BY customer_id
    ORDER BY order_date ASC
    LIMIT 1)t
```

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.LIMIT 1 不是“每个 customer 取 1 条”。
它是：整个查询结果只取 1 条。

2.外层思路没错，
主要是t.order_date=t.customer_pref_delivery_date这一段

```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT 
    ROUND(
        SUM(IF(order_date = customer_pref_delivery_date, 1, 0)) / COUNT(*) * 100,
        2
    ) AS immediate_percentage
FROM Delivery
WHERE (customer_id, order_date) IN (
    SELECT customer_id, MIN(order_date)
    FROM Delivery
    GROUP BY customer_id
);
```

==========================================
Conclusion
==========================================
```text

1.SQL 的思考顺序不要从 SELECT 开始，而是从数据处理流程开始：
FROM 表
WHERE 先筛行
GROUP BY 分组
HAVING 筛分组
SELECT 算结果/展示结果
ORDER BY 排序

2.什么时候计算放在 WHERE？
当你的问题是：
我要不要保留这一行？
这种就放在 WHERE。

什么时候计算放在 SELECT？
当你的问题是：
我不想筛掉行，我只是想计算一个结果。
这种就放在 SELECT。

3.子查询放在哪里，取决于它的结果要干什么。
如果子查询是用来“算一个值显示出来”，放 SELECT。
如果子查询是用来“决定哪些行留下”，放 WHERE。

```