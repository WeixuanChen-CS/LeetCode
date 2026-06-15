-- 【题目】❌1341. Movie Rating (Medium)
-- 【链接】https://leetcode.com/problems/movie-rating

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT u.name AS results 
FROM(
SELECT t.user_id,MAX(number)
FROM(
    SELECT user_id,count(user_id) as number
    FROM MovieRating
    GROUP BY user_id)t
JOIN Users u
ON t.user_id=u.user_id)
ORDER BY u.name

UNION ALL

SELECT u2.name AS results
FROM(
    SELECT t2.user_id,MAX(avge)
    FROM(
        SELECT user_id,AVG(rating) AS avge,created_at
        FROM MovieRating
        WHERE DATE_FORMAT(created_at,'%Y-%m')='2020-02'
        GROUP BY user_id)t2
JOIN Users u2
ON t2.user_id=u2.user_id)
ORDER BY u2.name
```

==========================================
Analysis
==========================================
```text
这题的错误主要有：

1.大致思路是对的，用UNION ALL把两个结果连接起来，但是每一部分都还有错误的地方

2.第一部分：
我用的是max，但是max有个缺点，就是取值的时候只会把那个值带出来，值所对应的id之类的东西不会跟着出来

第二部分:
首先是题目搞错，要返回的是电影的名字不是人名，所以join错表了
其次也是max的问题

```

```sql
-- ==========================================
-- Correct solution
-- ==========================================
(SELECT u.name AS results
FROM(
    SELECT user_id,count(*) as number
    FROM MovieRating
    GROUP BY user_id
    )t
JOIN Users u
ON t.user_id=u.user_id
ORDER BY number DESC, u.name ASC
limit 1)

UNION ALL

(SELECT m.title AS results
FROM(
    SELECT movie_id,AVG(rating) AS avge
    FROM MovieRating
    WHERE DATE_FORMAT(created_at,'%Y-%m')='2020-02'
    GROUP BY movie_id
    )t2
JOIN Movies m
ON t2.movie_id=m.movie_id
ORDER BY avge DESC, m.title
limit 1)
```

==========================================
Conclusion
==========================================
```text

1.相比于max和min，还有一个考虑就是对值进行从大到小或者从小到大排序，然后取第一个值，
拿到的也是max或者min之后的值，并且可以带出同一行其他信息

2.lexicographically的意思就是按字母顺序从小到大排序

3.WHERE里用到的东西不一定需要被SELECT出来
```