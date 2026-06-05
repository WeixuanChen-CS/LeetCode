-- 【题目】✅595. Big Countries(easy)
-- 【链接】https://leetcode.com/problems/big-countries/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT name,population,area
FROM World
WHERE area>=3000000
OR population>=25000000
```