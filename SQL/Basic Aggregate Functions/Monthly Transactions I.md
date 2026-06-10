-- 【题目】❌1193. Monthly Transactions I (Medium)
-- 【链接】https://leetcode.com/problems/monthly-transactions-i/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT month(trans_date),
        country,
        count(id) AS trans_count,
        count(IF(state='approved',id,0))AS approved_count,
        sum(amount) AS trans_total_amount,
        sum(IF(state='approved',amount,0)) AS approved_total_amount
FROM Transactions
GROUP BY month(trans_date),country
```

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.month(trans_date) 输出格式不符合题目,需要输出年份+月份

2.approved_count 这里不能用 COUNT(IF(..., id, 0))
而 COUNT() 的规则是：只要不是 NULL 就数。
0 不是 NULL，所以 declined 也会被数。

```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT DATE_FORMAT(trans_date,'%Y-%m') as month,
        country,
        count(id) AS trans_count,
        sum(state='approved')AS approved_count,
        sum(amount) AS trans_total_amount,
        sum(IF(state='approved',amount,0)) AS approved_total_amount
FROM Transactions
GROUP BY DATE_FORMAT(trans_date,'%Y-%m'),country
```

==========================================
Conclusion
==========================================
```text

1.COUNT(*)意思是：数当前组里有多少行。

2.DATE_FORMAT() 是 MySQL 里用来把日期转换成指定格式字符串的函数。
语法：DATE_FORMAT(date_column, '格式')
DATE_FORMAT(trans_date, '%Y-%m'):把 trans_date 这个日期转换成 年-月 格式。
%Y  四位年份，比如 2019
%y  两位年份，比如 19
%m  两位月份，比如 01, 02, 12
%c  月份数字，比如 1, 2, 12
%d  两位日期，比如 01, 09, 31

3.SUM(条件)：在 MySQL 里常用来数“满足条件的行数”。

```