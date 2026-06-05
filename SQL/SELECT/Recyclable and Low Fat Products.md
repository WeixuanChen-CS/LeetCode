-- 【题目】❌1757. Recyclable and Low Fat Products (Easy)
-- 【链接】https://leetcode.com/problems/recyclable-and-low-fat-products/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT product_id
FROM low_fats, recyclable
WHERE Type = Y
```

==========================================
Analysis
==========================================
```text
这题的错误主要有 4 类：表名和列名混淆、FROM 用法错误、WHERE 条件写错、字符串值没有加引号。
题目思考：
1. 要返回什么？
   返回 product_id。
2. 从哪张表查？
   从 Products 表查。
3. 筛选条件是什么？
   low_fats = 'Y'
   recyclable = 'Y'
4. 两个条件是什么关系？
   both，说明用 AND。
   SELECT 要返回的列
对应 SQL 模板就是：
FROM 表名
WHERE 条件1
  AND 条件2;
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
SELECT 后面写：你想返回的列
FROM 后面写：表名
WHERE 后面写：筛选条件
AND 表示：多个条件同时满足
字符串值要加引号，比如 'Y'
列名必须是题目表里真实存在的列

SELECT column_name
FROM table_name
WHERE condition1
  AND condition2;
```