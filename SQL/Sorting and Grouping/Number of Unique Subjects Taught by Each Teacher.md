-- 【题目】✅2356. Number of Unique Subjects Taught by Each Teacher(Easy)
-- 【链接】https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT teacher_id,
       COUNT(DISTINCT subject_id) AS cnt
FROM Teacher
GROUP BY teacher_id
```


