-- 【题目】✅1148.Article Views I(easy)
-- 【链接】https://leetcode.com/problems/article-views-i/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id=viewer_id
ORDER BY id ASC
```

==========================================
Conclusion
==========================================
```text
ORDER BY写在WHERE后面
ASC 升序，DESC降序
AS重起名字
DISTINCT去重:
SELECT DISTINCT column 去重返回结果
COUNT(DISTINCT column) 计算不同值的数量
```
