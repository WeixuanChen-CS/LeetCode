-- 【题目】✅1517. Find Users With Valid E-Mails(Easy)
-- 【链接】https://leetcode.com/problems/find-users-with-valid-e-mails

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT *
FROM Users
WHERE REGEXP_LIKE(
    mail,
    '^[A-Za-z][A-Za-z0-9_.-]*@leetcode\\.com$',
    'c'
);
```

==========================================
Conclusion
==========================================
```text
正则表达
```