-- 【题目】✅1729. Find Followers Count(Easy)
-- 【链接】https://leetcode.com/problems/find-followers-count/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT user_id,
        count(follower_id) AS followers_count
FROM Followers
GROUP BY user_id
ORDER BY user_id ASC
```
