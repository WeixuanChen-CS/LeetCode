-- 【题目】✅1484. Group Sold Products By The Date(Easy)
-- 【链接】https://leetcode.com/problems/group-sold-products-by-the-date

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT sell_date,
        count(DISTINCT product) AS num_sold,
        GROUP_CONCAT(DISTINCT product ORDER BY product SEPARATOR ',') AS products
FROM Activities
GROUP BY sell_date
ORDER BY sell_date
```

==========================================
Conclusion
==========================================
```text
显示分组之后的结果并用逗号连接：GROUP_CONCAT
```