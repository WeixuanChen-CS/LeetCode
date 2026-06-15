-- 【题目】❌626. Exchange Seats (Medium)
-- 【链接】https://leetcode.com/problems/exchange-seats

==========================================
Analysis
==========================================
```text
考察：条件语句
```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT 
        CASE
        WHEN id%2=1 AND id<(SELECT max(id) FROM Seat) THEN id+1
        WHEN id%2=0 THEN id-1
        ELSE id
        END AS id,
        student
FROM Seat
ORDER BY id
```

==========================================
Conclusion
==========================================
```text

1.交换座位的核心思想：1-〉2，2-〉1，
所以其实对于奇数id要+1，
对于偶数id要-1，
同时如果最后是奇数那id就不要变，所以只要使得小于最大id的奇数都+1就可以，这样到最后一个id如果是奇数，那就不变，如果是偶数，那就正常-1

```