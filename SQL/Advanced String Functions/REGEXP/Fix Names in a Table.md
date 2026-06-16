-- 【题目】✅1667. Fix Names in a Table(Easy)
-- 【链接】https://leetcode.com/problems/fix-names-in-a-table

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT user_id,
        CONCAT(UPPER(LEFT(name,1)),LOWER(SUBSTRING(name,2))) AS name
FROM Users
ORDER BY user_id

```

==========================================
Conclusion
==========================================
```text
理解CONCAT,UPPER,LOWER,LEFT,SUBSTRING用法
```