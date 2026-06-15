-- 【题目】❌1321. Restaurant Growth (Medium)
-- 【链接】https://leetcode.com/problems/restaurant-growth

```sql
-- ==========================================
-- Correct solution
-- ==========================================
WITH daily AS(
    SELECT visited_on,sum(amount) AS daily_amount
    from Customer
    GROUP BY visited_on
),
rolling AS(
    SELECT visited_on,
        sum(daily_amount) OVER(
        ORDER BY visited_on
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS amount,
        ROUND(
            sum(daily_amount) OVER(
            ORDER BY visited_on
            ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)/7
            ,2) AS average_amount,
        ROW_NUMBER() OVER(
            ORDER BY visited_on
        )AS rn
    FROM daily
)
SELECT visited_on,amount,average_amount
FROM rolling
WHERE rn>=7
```

==========================================
Conclusion
==========================================
```text

1.滑动窗口查询，一步一步拆清楚其实没有很难，就是步骤比较多

```