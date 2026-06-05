-- 【题目】❌1661. Average Time of Process per Machine (Easy)
-- 【链接】https://leetcode.com/problems/average-time-of-process-per-machine/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT 
    a1.machine_id,
    ROUND(AVG(a2.timestamp-a1.timestamp),3) AS processing_time
FROM Activity a1
JOIN Activity a2
ON a1.machine_id = a2.machine_id
AND a1.process_id = a2.process_id
WHERE a1.activity_type = 'start'
AND a2.activity_type = 'end'
GROUP BY a1.process_id
```

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.题目问的是每一台机器，所以应该按machine id分类

2.不理解AVG的作用

```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT a1.machine_id, ROUND(AVG(a1.timestamp-a2.timestamp),3) as processing_time
FROM Activity a1
JOIN Activity a2
ON a1.machine_id=a2.machine_id
AND a1.process_id=a2.process_id
WHERE a1.activity_type='end'
AND a2.activity_type='start'
GROUP BY a1.machine_id;
```

==========================================
Conclusion
==========================================
```text

1.AVG() = 对当前组里的每一行算出一个数字，然后求这些数字的平均值。
所需条件：a.括号里必须是数字或能算出数字的表达式
        b.每一行最好已经代表一个“统计单位”
        c.如果题目说“每个 xxx 的平均值”，通常要搭配 GROUP BY

2.总结做这道题的思路：
    a.同一个process有两行，timestamp分别是start和end
    b.所以这里需要想办法把start和end放在同一行，也就是用到自连接，同时限制两个表分别对应start和end
    c.同时注意题目要求是每台机器，所以必须按machine id去分类
    d.计算耗时，算平均值并保留三位小数

```