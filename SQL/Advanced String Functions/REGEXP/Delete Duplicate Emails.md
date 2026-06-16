-- 【题目】✅196. Delete Duplicate Emails(Easy)
-- 【链接】https://leetcode.com/problems/delete-duplicate-emails

```sql
-- ==========================================
-- My solution
-- ==========================================
DELETE p1
FROM Person p1
JOIN Person p2
ON p1.email=p2.email
WHERE p1.id>p2.id
```

==========================================
Conclusion
==========================================
```text
DELETE join之后的表的某行
```