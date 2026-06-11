-- 【题目】✅5619. Biggest Single Number(Easy)
-- 【链接】https://leetcode.com/problems/biggest-single-number

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT IFNULL(MAX(num),null) AS num
FROM(
    SELECT num
    FROM MyNumbers
    GROUP BY num
    HAVING count(*)=1)t
```
