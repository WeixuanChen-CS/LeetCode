-- 【题目】❌1907. Count Salary Categories (Medium)
-- 【链接】https://leetcode.com/problems/count-salary-categories

```sql
-- ==========================================
-- Correct solution
-- ==========================================
# Write your MySQL query statement below
SELECT 'Low Salary' AS category,
        count(*) AS accounts_count
FROM Accounts
Where income<20000 
UNION ALL
SELECT 'Average Salary' AS category,
        count(*) AS accounts_count
FROM Accounts
WHERE income BETWEEN 20000 AND 50000
UNION ALL
SELECT 'High Salary' AS category,
        count(*) AS accounts_count
FROM Accounts
Where income>50000
```

==========================================
Conclusion
==========================================
```text

1.根据题目重造列，分别造表选出并用UNION ALL合并

2.对于条件在一个区间内，应该写：
WHERE income BETWEEN 20000 AND 50000
或者：
WHERE income >= 20000 AND income <= 50000
而不是：WHERE 20000 < income < 50000

```