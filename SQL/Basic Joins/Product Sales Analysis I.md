-- 【题目】✅1068. Product Sales Analysis I(Easy)
-- 【链接】https://leetcode.com/problems/product-sales-analysis-i/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT product_name,year,price
FROM Sales s
JOIN Product p
ON s.product_id=p.product_id
```