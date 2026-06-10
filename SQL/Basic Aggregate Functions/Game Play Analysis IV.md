-- 【题目】❌550. Game Play Analysis IV (Medium)
-- 【链接】https://leetcode.com/problems/game-play-analysis-iv/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT ROUND(
    count(a2.player_id)/SELECT count(*) FROM Activity GROUP BY player_id,
    2) AS fraction
FROM Activity a1
JOIN Activity a2
ON a1.player_id=a2.player_id
AND a2.event_date=DATE_ADD(a1.event_date,INTERVAL 1 day)
```

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.语法错：子查询不能直接写在除号后面

2.逻辑错：题目不是找“任意连续两天登录”
题目要求的是：
玩家在首次登录的第二天有没有再次登录。
我写的表示：
只要这个玩家有任意一次连续两天登录，就会被算进去。

3.然后我尝试这样写：AND a2.event_date=DATE_ADD(a1.MIN(event_date),INTERVAL 1 day)，这样写依然错
MIN() 不能直接放在 JOIN ON 里这样用
JOIN ON 是在一行一行配对的时候执行的。
这个阶段，SQL 正在拿 a1 的某一行和 a2 的某一行比较。
MIN(event_date)是要看完一个 player 的多行之后，才能算出最小日期。
所以逻辑顺序冲突了：
JOIN ON：还在逐行匹配
MIN(event_date)：需要先分组/聚合后才能得到
所以你不能在 ON 里直接写“这个 player 的最小 event_date”。
你可以把它记成：
如果我要用 MIN/MAX/COUNT 这种“每组算出来的结果”，
通常要先在子查询里算出来，
再在外层 JOIN / WHERE / SELECT 里使用。

```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
# Write your MySQL query statement below
SELECT ROUND(
    count(a.player_id)/count(t.player_id)
    ,2) AS fraction
FROM(
    SELECT player_id, MIN(event_date) AS first_login
    FROM Activity 
    GROUP BY player_id
)t
LEFT JOIN Activity a
ON a.player_id=t.player_id
AND a.event_date=DATE_ADD(t.first_login,interval 1 Day)

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