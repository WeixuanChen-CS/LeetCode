-- 【题目】❌180. Consecutive Numbers (Medium)
-- 【链接】https://leetcode.com/problems/consecutive-numbers

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.压根没写出来，对于要取连续的三个数完全不知道要怎么办

```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT DISTINCT l1.num AS ConsecutiveNums
FROM Logs l1
JOIN Logs l2
ON l1.id+1=l2.id
JOIN Logs l3
ON l2.id+1=l3.id
WHERE l1.num=l2.num
AND l2.num=l3.num
```

==========================================
Conclusion
==========================================
```text

1.写法和写代码证明arr[i] == arr[i + 1] == arr[i + 2]很像，
但是sql没有直接的 arr[i+1]，所以用 self join 把“相邻行”横向拼起来。

```