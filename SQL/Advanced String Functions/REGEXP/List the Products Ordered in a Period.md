-- 【题目】✅1327. List the Products Ordered in a Period(Easy)
-- 【链接】https://leetcode.com/problems/list-the-products-ordered-in-a-period

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT p.product_name,
        sum(unit) AS unit
FROM Products p
LEFT JOIN Orders o
ON p.product_id=o.product_id
WHERE DATE_FORMAT(order_date,'%Y-%m')='2020-02'
GROUP BY p.product_name
HAVING sum(unit)>=100
```