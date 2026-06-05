-- 【题目】✅620. Not Boring Movies(Easy)
-- 【链接】https://leetcode.com/problems/not-boring-movies/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT id,movie,description,rating
FROM Cinema
WHERE id%2=1
AND description!='boring'
ORDER BY rating DESC
```

==========================================
Conclusion
==========================================
```text
判断奇偶：
值%2=1奇
值%2=0偶
```