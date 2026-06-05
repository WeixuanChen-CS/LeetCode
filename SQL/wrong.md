-- 【题目】❌1757. Recyclable and Low Fat Products (Easy)
-- 【链接】https://leetcode.com/problems/recyclable-and-low-fat-products/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT product_id
FROM low_fats, recyclable
WHERE Type = Y
```

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.比反了，题目要的是今天的温度比前一天高

2.题目要求的是：
previous dates / yesterday
所以更好的做法是用record date而不是id去做比较，
并且要限制上一行的日期是昨天，因为也有可能是前天

```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT product_id
from Products
Where low_fats='Y'
AND recyclable='Y'
```

==========================================
Conclusion
==========================================
```text

1.子查询：select from后面又接一个select from，从第二个表中搜查需要的信息，写的时候记得给子表命名

2.LAG的用法：LAG（）：取上一行的值，
比如LAG(column) OVER (ORDER BY id)
按 id 排序后，取上一行的 column，
同理还有LEAD()：取下一行的值

3.DATEDIFF（）用来计算天数差
DATEDIFF（D1，D2）是D1-D2
同时用DATE_ADD 和 DATE_SUB 也可以做到对日期（年月日小时分钟秒都可以）做加减法
DATE_ADD/SUB(日期, INTERVAL 数字 单位)
对于这道题，以下三个语法表达同一个意思：
DATE_SUB(recordDate, INTERVAL 1 DAY) = pre_d
DATE_ADD(pre_d, INTERVAL 1 DAY) = recordDate
DATEDIFF(recordDate, pre_d) = 1

```