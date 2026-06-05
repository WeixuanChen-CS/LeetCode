-- 【题目】❌584. Find Customer Referee (Easy)
-- 【链接】https://leetcode.com/problems/find-customer-referee/

```sql
-- ==========================================
-- My solution 
-- ==========================================
SELECT name
FROM Customer
WHERE referee_id!=2
OR referee_id=null
```

==========================================
Analysis
==========================================
```text
判断 NULL：用 IS NULL
判断非 NULL：用 IS NOT NULL
```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT name
FROM Customer
WHERE referee_id!=2
OR referee_id is null
```