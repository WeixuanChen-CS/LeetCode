-- 【题目】❌602. Friend Requests II: Who Has the Most Friends (Meidum)
-- 【链接】https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT id,count(*) AS num
FROM(
    SELECT requester_id AS id FROM RequestAccepted
    UNION ALL
    SELECT accepter_id AS id FROM RequestAccepted
)t
GROUP BY id
ORDER BY num DESC
limit 1
```

==========================================
Conclusion
==========================================
```text

1.这题最难的部分就是理解题意，到底怎么样才算有朋友
其实对于每一组request和accept，代表这两个人都收获了一个朋友
所以把两组的id放在同一列里收集起来，然后分组再计算数量，一个人的名字出现了几次就代表对方有几个朋友，就可以得到每个人的朋友数
然后倒序排列取第一个就是朋友数量最多的
```