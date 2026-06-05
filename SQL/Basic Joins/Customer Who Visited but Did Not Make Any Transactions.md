-- 【题目】❌1581. Customer Who Visited but Did Not Make Any Transactions (Easy)
-- 【链接】https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT customer_id,COUNT(amount is null) AS count_no_trans
FROM Visits V
LEFT JOIN Transactions T
ON V.visit_id=T.visit_id
```

==========================================
Analysis
==========================================
```text
1.count的用法并未理解导致用错
例：
transaction_id
--------------
12
13
NULL
NULL
NULL

当你写transaction_id is null，会变成：
transaction_id | transaction_id IS NULL
---------------|------------------------
12             | 0
13             | 0
NULL           | 1
NULL           | 1
NULL           | 1

其中0&1都不是null，所以count（transaction_id is null）会得到5
2.没有想到要分组，对于相同customer_id，有的顾客来了好几次，有的时候有交易有的时候没有，并且每种情况都可能出现多次
3.对于null值的计数，要先筛选再计数
```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT customer_id,COUNT(*) AS count_no_trans
FROM Visits V
LEFT JOIN Transactions T
ON V.visit_id=T.visit_id
WHERE transaction_id is null
GROUP BY customer_id
```

==========================================
Conclusion
==========================================
```text
GROUP BY:把相同值的行分成一组
COUNT(*):数当前结果里有多少行
COUNT(表达式) 不是数多少表达式 true，而是数多少表达式非 NULL。
```