==================================================
1. SELECT：查询数据
==================================================

语法：

SELECT column1, column2
FROM table_name;

作用：
从一张表中选择想要查询的列。

含义：
SELECT 后面写你想看的列。
FROM 后面写数据来自哪张表。

例子：

SELECT name, age
FROM students;

解释：
从 students 表中查询 name 和 age 两列。

如果想查询所有列，可以写：

SELECT *
FROM students;

解释：
* 表示所有列。
这个语句表示查询 students 表中的全部数据。


==================================================
2. WHERE：条件筛选
==================================================

语法：

SELECT column1, column2
FROM table_name
WHERE condition;

作用：
只查询满足条件的数据。

含义：
WHERE 后面写筛选条件，只有满足条件的行才会被返回。

例子：

SELECT *
FROM students
WHERE age > 20;

解释：
查询 students 表中年龄大于 20 岁的学生。

常见条件写法：

age = 20        表示 age 等于 20
age != 20       表示 age 不等于 20
age > 20        表示 age 大于 20
age >= 20       表示 age 大于等于 20
age < 20        表示 age 小于 20
age <= 20       表示 age 小于等于 20

多个条件可以用 AND 或 OR。

例子：

SELECT *
FROM students
WHERE age > 20 AND major = 'CS';

解释：
查询年龄大于 20，并且专业是 CS 的学生。
AND 表示两个条件都必须满足。

例子：

SELECT *
FROM students
WHERE major = 'CS' OR major = 'Math';

解释：
查询专业是 CS 或 Math 的学生。
OR 表示满足其中一个条件即可。


==================================================
3. ORDER BY：排序
==================================================

语法：

SELECT column1, column2
FROM table_name
ORDER BY column_name ASC;

作用：
按照某一列对查询结果进行排序。

含义：
ORDER BY 后面写排序依据。
ASC 表示升序，从小到大。
DESC 表示降序，从大到小。

例子：

SELECT *
FROM students
ORDER BY age ASC;

解释：
按照 age 从小到大排序。

例子：

SELECT *
FROM students
ORDER BY age DESC;

解释：
按照 age 从大到小排序。

注意：
如果不写 ASC 或 DESC，默认是 ASC，也就是升序。


==================================================
4. LIMIT：限制返回数量
==================================================

语法：

SELECT column1, column2
FROM table_name
LIMIT number;

作用：
限制查询结果返回的行数。

含义：
LIMIT 5 表示只返回前 5 条记录。

例子：

SELECT *
FROM students
LIMIT 5;

解释：
只查询 students 表中的前 5 条数据。


==================================================
5. DISTINCT：去重
==================================================

语法：

SELECT DISTINCT column_name
FROM table_name;

作用：
去掉重复值，只显示不同的结果。

含义：
如果一列中有很多重复值，DISTINCT 可以只保留唯一值。

例子：

SELECT DISTINCT major
FROM students;

解释：
查询 students 表中有哪些不同的专业。
如果有很多学生都是 CS，只会显示一次 CS。


==================================================
6. LIKE：模糊查询
==================================================

语法：

SELECT column1, column2
FROM table_name
WHERE column_name LIKE pattern;

作用：
按照字符串模式进行模糊查询。

含义：
LIKE 常用于查询名字、邮箱、文本等字段。
% 表示任意多个字符。

常见写法：

LIKE 'A%'       表示以 A 开头
LIKE '%son'     表示以 son 结尾
LIKE '%an%'     表示中间包含 an

例子：

SELECT *
FROM students
WHERE name LIKE 'A%';

解释：
查询名字以 A 开头的学生。
比如 Alice、Amy 都符合。

例子：

SELECT *
FROM students
WHERE name LIKE '%an%';

解释：
查询名字中包含 an 的学生。
比如 Andy、Daniel 都可能符合。


==================================================
7. BETWEEN：范围查询
==================================================

语法：

SELECT column1, column2
FROM table_name
WHERE column_name BETWEEN value1 AND value2;

作用：
查询某个范围内的数据。

含义：
BETWEEN A AND B 表示在 A 和 B 之间，包括 A 和 B。

例子：

SELECT *
FROM students
WHERE age BETWEEN 18 AND 25;

解释：
查询年龄在 18 到 25 岁之间的学生。
包括 18 岁和 25 岁。

等价于：

SELECT *
FROM students
WHERE age >= 18 AND age <= 25;


==================================================
8. IN：匹配多个值
==================================================

语法：

SELECT column1, column2
FROM table_name
WHERE column_name IN (value1, value2, value3);

作用：
判断某一列的值是否属于指定的一组值。

含义：
IN 可以简化多个 OR 条件。

例子：

SELECT *
FROM students
WHERE major IN ('CS', 'Math', 'Physics');

解释：
查询专业是 CS、Math 或 Physics 的学生。

等价于：

SELECT *
FROM students
WHERE major = 'CS'
   OR major = 'Math'
   OR major = 'Physics';


==================================================
9. NULL：空值判断
==================================================

语法：

SELECT column1, column2
FROM table_name
WHERE column_name IS NULL;

作用：
判断某一列是否为空。

含义：
NULL 表示没有值，不是 0，也不是空字符串。
判断 NULL 不能用 = NULL，必须用 IS NULL。

例子：

SELECT *
FROM students
WHERE email IS NULL;

解释：
查询没有填写 email 的学生。

例子：

SELECT *
FROM students
WHERE email IS NOT NULL;

解释：
查询填写了 email 的学生。


==================================================
10. COUNT：计数
==================================================

语法：

SELECT COUNT(*)
FROM table_name;

作用：
统计有多少条记录。

含义：
COUNT(*) 表示统计行数。

例子：

SELECT COUNT(*)
FROM students;

解释：
统计 students 表中一共有多少个学生。

例子：

SELECT major, COUNT(*) AS student_count
FROM students
GROUP BY major;

解释：
按照 major 分组，统计每个专业有多少学生。
AS student_count 是给统计结果起别名，方便阅读。


==================================================
11. SUM：求和
==================================================

语法：

SELECT SUM(column_name)
FROM table_name;

作用：
计算某一列的总和。

含义：
SUM 通常用于数字列，比如分数、金额、数量等。

例子：

SELECT SUM(score)
FROM exams;

解释：
计算 exams 表中所有 score 的总和。


==================================================
12. AVG：求平均值
==================================================

语法：

SELECT AVG(column_name)
FROM table_name;

作用：
计算某一列的平均值。

含义：
AVG 通常用于数字列。

例子：

SELECT AVG(score)
FROM exams;

解释：
计算所有学生考试分数的平均值。


==================================================
13. MAX 和 MIN：最大值和最小值
==================================================

语法：

SELECT MAX(column_name)
FROM table_name;

SELECT MIN(column_name)
FROM table_name;

作用：
MAX 用来查询最大值。
MIN 用来查询最小值。

例子：

SELECT MAX(score)
FROM exams;

解释：
查询最高分。

例子：

SELECT MIN(score)
FROM exams;

解释：
查询最低分。


==================================================
14. GROUP BY：分组
==================================================

语法：

SELECT column_name, aggregate_function(column_name)
FROM table_name
GROUP BY column_name;

作用：
按照某一列进行分组，然后对每组进行统计。

含义：
GROUP BY 通常和 COUNT、SUM、AVG、MAX、MIN 一起使用。

例子：

SELECT major, COUNT(*) AS student_count
FROM students
GROUP BY major;

解释：
按照专业分组，统计每个专业有多少学生。

例子：

SELECT major, AVG(age) AS avg_age
FROM students
GROUP BY major;

解释：
按照专业分组，计算每个专业学生的平均年龄。


==================================================
15. HAVING：分组后筛选
==================================================

语法：

SELECT column_name, aggregate_function(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;

作用：
对 GROUP BY 分组后的结果进行筛选。

含义：
WHERE 是分组之前筛选原始数据。
HAVING 是分组之后筛选统计结果。

例子：

SELECT major, COUNT(*) AS student_count
FROM students
GROUP BY major
HAVING COUNT(*) > 10;

解释：
先按照专业分组，统计每个专业人数。
然后只保留人数超过 10 的专业。

WHERE 和 HAVING 的区别：

WHERE age > 18
表示先筛选出年龄大于 18 的学生。

HAVING COUNT(*) > 10
表示分组统计之后，只保留人数超过 10 的组。

完整例子：

SELECT major, COUNT(*) AS student_count
FROM students
WHERE age > 18
GROUP BY major
HAVING COUNT(*) > 10;

解释：
第一步：从 students 表中查询。
第二步：先筛选年龄大于 18 的学生。
第三步：按照 major 分组。
第四步：统计每个专业的人数。
第五步：只保留人数超过 10 的专业。


==================================================
16. AS：起别名
==================================================

语法：

SELECT column_name AS alias_name
FROM table_name;

作用：
给列名或表名起一个临时名字。

含义：
AS 可以让查询结果更清楚，也可以让表名更短。

例子：

SELECT COUNT(*) AS student_count
FROM students;

解释：
把 COUNT(*) 的结果命名为 student_count。

例子：

SELECT s.name, s.age
FROM students AS s;

解释：
把 students 表临时命名为 s。
之后可以用 s.name 表示 students 表中的 name 列。

AS 也可以省略：

SELECT s.name, s.age
FROM students s;


==================================================
17. JOIN：连接两张表
==================================================

语法：

SELECT columns
FROM table1
JOIN table2
ON table1.common_column = table2.common_column;

作用：
把两张表根据共同字段连接起来查询。

含义：
JOIN 用于多表查询。
ON 后面写两张表之间的匹配条件。

假设有两张表：

students 表：

student_id | name
1          | Alice
2          | Bob

grades 表：

student_id | course | grade
1          | SQL    | A
2          | Python | B

例子：

SELECT s.name, g.course, g.grade
FROM students s
JOIN grades g
ON s.student_id = g.student_id;

解释：
students 表和 grades 表都有 student_id。
通过 student_id 把两张表连接起来。
最后查询学生姓名、课程和成绩。


==================================================
18. INNER JOIN：内连接
==================================================

语法：

SELECT columns
FROM table1
INNER JOIN table2
ON table1.id = table2.id;

作用：
只保留两张表中都能匹配上的数据。

含义：
如果左表有数据，但右表没有匹配记录，就不会显示。
如果右表有数据，但左表没有匹配记录，也不会显示。

例子：

SELECT s.name, g.course, g.grade
FROM students s
INNER JOIN grades g
ON s.student_id = g.student_id;

解释：
只查询有成绩记录的学生。
没有成绩的学生不会显示。


==================================================
19. LEFT JOIN：左连接
==================================================

语法：

SELECT columns
FROM table1
LEFT JOIN table2
ON table1.id = table2.id;

作用：
保留左表所有数据，右表没有匹配时显示 NULL。

含义：
LEFT JOIN 以左表为主。
即使右表没有对应数据，左表的数据也会显示。

例子：

SELECT s.name, g.course, g.grade
FROM students s
LEFT JOIN grades g
ON s.student_id = g.student_id;

解释：
查询所有学生。
如果某个学生没有成绩，也会显示这个学生，只是 course 和 grade 会显示 NULL。


==================================================
20. RIGHT JOIN：右连接
==================================================

语法：

SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.id = table2.id;

作用：
保留右表所有数据，左表没有匹配时显示 NULL。

含义：
RIGHT JOIN 以右表为主。
即使左表没有对应数据，右表的数据也会显示。

例子：

SELECT s.name, g.course, g.grade
FROM students s
RIGHT JOIN grades g
ON s.student_id = g.student_id;

解释：
保留 grades 表中的所有成绩记录。
即使某条成绩找不到对应学生，也会显示出来。


==================================================
21. FULL JOIN：全连接
==================================================

语法：

SELECT columns
FROM table1
FULL JOIN table2
ON table1.id = table2.id;

作用：
保留左右两张表的所有数据。

含义：
两张表能匹配上的就合并。
匹配不上的也显示，缺失的部分用 NULL 填充。

例子：

SELECT s.name, g.course, g.grade
FROM students s
FULL JOIN grades g
ON s.student_id = g.student_id;

解释：
students 和 grades 两张表中的所有记录都会显示。
能匹配上的显示在同一行。
不能匹配的地方显示 NULL。

注意：
MySQL 不直接支持 FULL JOIN。
PostgreSQL 支持 FULL JOIN。


==================================================
22. 子查询 Subquery
==================================================

语法：

SELECT columns
FROM table_name
WHERE column_name > (
    SELECT aggregate_function(column_name)
    FROM table_name
);

作用：
在一个查询里面嵌套另一个查询。

含义：
子查询会先执行，然后外层查询使用子查询的结果。

例子：

SELECT *
FROM students
WHERE age > (
    SELECT AVG(age)
    FROM students
);

解释：
第一步：子查询先计算所有学生的平均年龄。
第二步：外层查询找出年龄大于平均年龄的学生。


==================================================
23. INSERT INTO：插入数据
==================================================

语法：

INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3);

作用：
向表中添加新数据。

含义：
INSERT INTO 后面写表名和列名。
VALUES 后面写对应的值。

例子：

INSERT INTO students (student_id, name, age, major)
VALUES (1, 'Alice', 20, 'CS');

解释：
向 students 表中插入一条学生记录。
student_id 是 1，name 是 Alice，age 是 20，major 是 CS。


==================================================
24. UPDATE：更新数据
==================================================

语法：

UPDATE table_name
SET column_name = new_value
WHERE condition;

作用：
修改表中已有的数据。

含义：
UPDATE 后面写要修改的表。
SET 后面写要修改哪一列以及新值。
WHERE 后面写修改哪几行。

例子：

UPDATE students
SET major = 'Data Science'
WHERE student_id = 1;

解释：
把 student_id 为 1 的学生的 major 改成 Data Science。

重要提醒：
UPDATE 一定要小心写 WHERE。
如果不写 WHERE，可能会修改整张表。

危险例子：

UPDATE students
SET major = 'Data Science';

解释：
这个语句会把所有学生的专业都改成 Data Science。
这通常不是你想要的结果。


==================================================
25. DELETE：删除数据
==================================================

语法：

DELETE FROM table_name
WHERE condition;

作用：
删除表中的某些数据。

含义：
DELETE FROM 后面写表名。
WHERE 后面写删除条件。

例子：

DELETE FROM students
WHERE student_id = 1;

解释：
删除 student_id 为 1 的学生记录。

重要提醒：
DELETE 一定要小心写 WHERE。
如果不写 WHERE，会删除整张表中的所有数据。

危险例子：

DELETE FROM students;

解释：
删除 students 表中的所有记录。
表还在，但是表里的数据都没了。


==================================================
26. CREATE TABLE：创建表
==================================================

语法：

CREATE TABLE table_name (
    column1 data_type constraint,
    column2 data_type constraint,
    column3 data_type constraint
);

作用：
创建一张新的数据表。

含义：
CREATE TABLE 后面写表名。
括号里面写每一列的名字、数据类型和约束条件。

例子：

CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    major VARCHAR(100),
    email VARCHAR(100)
);

解释：
创建一张 students 表。
这张表有五列：
student_id：学生 ID，是整数，并且是主键。
name：学生姓名，字符串，最多 100 个字符。
age：年龄，整数。
major：专业，字符串，最多 100 个字符。
email：邮箱，字符串，最多 100 个字符。


==================================================
27. 常见数据类型
==================================================

INT：
整数。
例子：1, 20, 100

VARCHAR(n)：
字符串，最多 n 个字符。
例子：VARCHAR(100) 表示最多 100 个字符。

DATE：
日期。
例子：2026-06-02

FLOAT：
小数。
例子：3.14, 98.5

BOOLEAN：
布尔值。
通常表示 True 或 False。


==================================================
28. PRIMARY KEY：主键
==================================================

语法：

CREATE TABLE table_name (
    id INT PRIMARY KEY,
    column_name data_type
);

作用：
唯一标识表中的每一条记录。

含义：
主键不能重复，也不能是 NULL。
一张表通常会有一个主键。

例子：

CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT
);

解释：
student_id 是主键。
每个学生都有唯一的 student_id。


==================================================
29. FOREIGN KEY：外键
==================================================

语法：

CREATE TABLE table2 (
    id INT PRIMARY KEY,
    table1_id INT,
    FOREIGN KEY (table1_id) REFERENCES table1(id)
);

作用：
建立两张表之间的关系。

含义：
外键表示这张表中的某一列，引用了另一张表的主键。

例子：

CREATE TABLE grades (
    grade_id INT PRIMARY KEY,
    student_id INT,
    course VARCHAR(100),
    grade VARCHAR(10),
    FOREIGN KEY (student_id) REFERENCES students(student_id)
);

解释：
grades 表中的 student_id 是外键。
它引用 students 表中的 student_id。
意思是：每条成绩记录都对应某个学生。


==================================================
30. ALTER TABLE：修改表结构
==================================================

语法：

ALTER TABLE table_name
ADD column_name data_type;

作用：
修改已经存在的表结构，比如增加列、删除列、修改列类型。

增加一列：

ALTER TABLE students
ADD phone VARCHAR(20);

解释：
给 students 表增加 phone 这一列。

删除一列：

ALTER TABLE students
DROP COLUMN phone;

解释：
删除 students 表中的 phone 这一列。


==================================================
31. DROP TABLE：删除表
==================================================

语法：

DROP TABLE table_name;

作用：
删除整张表。

含义：
DROP TABLE 会删除表结构和表里的所有数据。
这个操作比 DELETE 更危险。

例子：

DROP TABLE students;

解释：
删除 students 这张表。
表和表里的数据都会消失。

==================================================
32. LAG()：取当前行的上一行的值
==================================================
语法：
LAG(column) OVER (ORDER BY id)
按 id 排序后，取上一行的 column

==================================================
33. DATEDIFF：计算相差天数
==================================================
DATEDIFF(date1, date2)：date1 - date2 的天数差

例：
DATEDIFF('2015-01-02', '2015-01-01')，
返回 1

==================================================
34. SELF JOIN
==================================================
SELECT ...
FROM 表名 a
JOIN 表名 b
ON a.某列 = b.某列;

==================================================
35. 判断奇偶数
==================================================
判断奇数：列名 % 2 = 1
判断偶数：列名 % 2 = 0

==================================================
36. DATE_ADD
==================================================
DATE_ADD(日期, INTERVAL 数字 单位)
最常用的是加一天：
DATE_ADD(event_date, INTERVAL 1 DAY)
意思是：
event_date + 1 天
其他单位也可以：
DATE_ADD(date_col, INTERVAL 7 DAY)    -- 加 7 天
DATE_ADD(date_col, INTERVAL 1 MONTH)  -- 加 1 个月
DATE_ADD(date_col, INTERVAL 1 YEAR)   -- 加 1 年
DATE_ADD(date_col, INTERVAL 2 HOUR)   -- 加 2 小时
如果是减一天，可以写：
DATE_SUB(event_date, INTERVAL 1 DAY)

==================================================
37. IFNULL：返回空值
==================================================
IFNULL(MAX(num), NULL)

==================================================
38. IF条件
==================================================
IF(条件, 条件成立时返回的值, 条件不成立时返回的值)
也就是：
IF(condition, value_if_true, value_if_false)

==================================================
39. 窗口函数
==================================================
窗口函数是在“不把行合并掉”的情况下，给每一行额外算一个值。
最基本语法：
函数名() OVER (
    PARTITION BY 分组列
    ORDER BY 排序列
)

PARTITION BY 是什么？
PARTITION BY 可以理解成：
在每个组里面分别做窗口函数。

你看到这些关键词，可以优先想窗口函数：
题目关键词	常用窗口函数
累计、running total、连续相加	SUM() OVER
每组第一条 / 最新一条 / 最早一条	ROW_NUMBER() OVER
排名、第几名	RANK() / DENSE_RANK()
上一天 / 上一条 / 下一条	LAG() / LEAD()
不想让 GROUP BY 合并行，但又想算组内结果	窗口函数

==================================================
40. limit：限定行数
==================================================
limit：1  ： 只拿第一行

==================================================
41. union all：拼接表
==================================================
UNION ALL 的意思是：
把多个 SELECT 的结果 上下拼接起来，并且保留重复行。

==================================================
42. 手动造行
==================================================
手动造一行的基本语法是：

==================================================
43. case when
==================================================
CASE WHEN 是 SQL 里的条件判断语句
SELECT 固定值 AS 列名;
CASE
    WHEN 条件1 THEN 结果1
    WHEN 条件2 THEN 结果2
    ELSE 其他结果
END

==================================================
44. 滑动窗口
==================================================
SQL 里的“滑动窗口”本质是：
按某个顺序排列后，对每一行，只看它附近的一段范围，然后做 SUM / AVG / COUNT 等计算。
它属于窗口函数的一部分。
语法：
聚合函数(列名) OVER (
    PARTITION BY 分组列
    ORDER BY 排序列
    ROWS BETWEEN 前面/后面几行 PRECEDING/FOLLOWING AND CURRENT ROW
)
最常见：
SUM(amount) OVER (
    ORDER BY visited_on
    ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
)
按照 visited_on 排序
对每一行，取当前行 + 前面 6 行
然后求 SUM(amount)
也就是 7 行滑动窗口。
PARTITION BY：如果你要每个组内部单独滑动，就加 PARTITION BY

==================================================
45. WITH...AS
==================================================
给一个临时查询结果起名字，后面像表一样使用。
WITH 临时表1 AS (
    SELECT ...
),
临时表2 AS (
    SELECT ...
),
临时表3 AS (
    SELECT ...
)
SELECT ...
FROM 临时表3;

==================================================
45. ROW_NUMBER()
==================================================
ROW_NUMBER()窗口函数
按你指定的顺序，给每一行编号：1, 2, 3, 4...
ROW_NUMBER() OVER (
    ORDER BY 排序列
) AS 新列名

==================================================
45. DENSE_RANK()
==================================================
DENSE_RANK()是一个窗口排名函数
它的作用是：
按某个列排序后，给每一行排名；如果值一样，就给相同排名；下一个名次不会跳号
ROW_NUMBER()	不管并列，强行编号	    1, 2, 3, 4
RANK()	        并列同名次，但会跳号	1, 2, 2, 4
DENSE_RANK()	并列同名次，不跳号	    1, 2, 2, 3
窗口函数要作为一列放进查询结果里










==================================================
SQL题目类型
==================================================
1. 条件聚合题
看到这种词：
count of approved
total amount
percentage
rate
ratio
average

通常是：
SUM(IF(condition, 1, 0))
SUM(IF(condition, amount, 0))
COUNT(*)
ROUND(...)
代表题目不是筛掉某些行，而是保留所有行，在 SELECT 里条件计算。

2. 先找“每组第一/最大/最小”的题
看到这种词：
first
earliest
latest
maximum
minimum
most recent
highest

你要立刻想到：
GROUP BY xxx
MIN(...)
MAX(...)

或者：
ROW_NUMBER() OVER (
    PARTITION BY xxx
    ORDER BY xxx
)
这类题的核心不是最终计算，而是先造出：
每组对应的目标行

比如：
每个 customer 的第一单
每个 product 的最高价格
每个 user 的最近登录

3. 分组后再筛的题
看到这种：
users with at least 5 orders
products sold more than 100 units
classes with more than 5 students

你要想到：
GROUP BY ...
HAVING COUNT(*) >= ...
不是 WHERE COUNT(*)。

4. 两张表关联题
看到题目给两张表，比如：
Users + Orders
Employees + Departments
Products + Sales

你先问：
最终结果的主体是谁？
比如结果要列出所有 users，即使没有订单，也要：
LEFT JOIN
如果只关心有匹配记录的，通常：
JOIN

==================================================
做题前思考
==================================================
题目目标：要求输出什么？
分母/主体：最终结果基于哪些行？
第一步中间表：需要先 group / filter / join 出什么？
第二步中间表：筛完后表长什么样？
最终计算：SELECT 里算什么？
容易误放 WHERE 的条件：哪些条件只是算分子，不能筛掉？
























==================================================
32. 最常用 SQL 查询模板
==================================================

语法模板：

SELECT column1, column2, aggregate_function(column3)
FROM table_name
JOIN another_table
ON table_name.id = another_table.id
WHERE condition
GROUP BY column1, column2
HAVING aggregate_condition
ORDER BY column1 DESC
LIMIT 10;

逐行解释：

SELECT：
选择最终要显示的列。

FROM：
说明数据来自哪张表。

JOIN：
连接另一张表。

ON：
说明两张表通过哪个字段匹配。

WHERE：
在分组前筛选原始数据。

GROUP BY：
按照某些列进行分组。

HAVING：
对分组后的结果进行筛选。

ORDER BY：
对最终结果排序。

LIMIT：
限制返回多少条结果。


==================================================
33. SQL 的书写顺序和执行顺序
==================================================

SQL 常见书写顺序：

SELECT
FROM
JOIN
ON
WHERE
GROUP BY
HAVING
ORDER BY
LIMIT

但是 SQL 的实际执行顺序大概是：

1. FROM / JOIN
2. ON
3. WHERE
4. GROUP BY
5. HAVING
6. SELECT
7. ORDER BY
8. LIMIT

解释：
虽然 SELECT 写在最前面，但数据库通常不是最先执行 SELECT。
它会先找到数据来源，再筛选，再分组，再选择要显示的列。


==================================================
34. 完整例子 1：基础查询
==================================================

问题：
查询所有 CS 专业，并且年龄大于 20 岁的学生，按照年龄从大到小排序。

SQL：

SELECT *
FROM students
WHERE major = 'CS' AND age > 20
ORDER BY age DESC;

解释：
FROM students：从 students 表查询。
WHERE major = 'CS' AND age > 20：只保留专业是 CS 且年龄大于 20 的学生。
ORDER BY age DESC：按照年龄从大到小排序。
SELECT *：显示所有列。


==================================================
35. 完整例子 2：分组统计
==================================================

问题：
统计每个专业有多少学生，并且只显示人数超过 10 的专业。

SQL：

SELECT major, COUNT(*) AS student_count
FROM students
GROUP BY major
HAVING COUNT(*) > 10;

解释：
FROM students：从 students 表中查询。
GROUP BY major：按照专业分组。
COUNT(*)：统计每个专业的人数。
AS student_count：把统计结果命名为 student_count。
HAVING COUNT(*) > 10：只显示人数超过 10 的专业。


==================================================
36. 完整例子 3：多表连接
==================================================

问题：
查询每个学生的姓名、课程和成绩。

SQL：

SELECT s.name, g.course, g.grade
FROM students s
JOIN grades g
ON s.student_id = g.student_id;

解释：
students s：把 students 表临时命名为 s。
grades g：把 grades 表临时命名为 g。
JOIN grades g：连接 grades 表。
ON s.student_id = g.student_id：通过 student_id 匹配两张表。
SELECT s.name, g.course, g.grade：显示学生姓名、课程和成绩。


==================================================
37. 完整例子 4：子查询
==================================================

问题：
查询分数高于平均分的考试记录。

SQL：

SELECT *
FROM exams
WHERE score > (
    SELECT AVG(score)
    FROM exams
);

解释：
子查询 SELECT AVG(score) FROM exams 先计算平均分。
外层查询再找出 score 大于平均分的记录。


==================================================
38. 入门最重要的 SQL 口诀
==================================================

查什么，用 SELECT。
从哪查，用 FROM。
筛行数，用 WHERE。
要分组，用 GROUP BY。
筛分组，用 HAVING。
要排序，用 ORDER BY。
看前几条，用 LIMIT。
连多表，用 JOIN。
插数据，用 INSERT。
改数据，用 UPDATE。
删数据，用 DELETE。
建表，用 CREATE TABLE。


==================================================
39. 最应该优先背下来的核心语法
==================================================

SELECT ...
FROM ...
WHERE ...
GROUP BY ...
HAVING ...
ORDER BY ...
LIMIT ...;

含义：

SELECT：查哪些列
FROM：从哪张表查
WHERE：筛选哪些行
GROUP BY：按照什么分组
HAVING：筛选分组后的结果
ORDER BY：按照什么排序
LIMIT：只返回前几条


==================================================
40. 常见易错点
==================================================

易错点 1：
判断空值不能写 = NULL。

错误：

WHERE email = NULL

正确：

WHERE email IS NULL


易错点 2：
UPDATE 和 DELETE 一定要写 WHERE。

危险：

UPDATE students
SET major = 'CS';

这会修改所有学生。

危险：

DELETE FROM students;

这会删除整张表里的所有数据。


易错点 3：
WHERE 和 HAVING 不一样。

WHERE：
分组前筛选原始行。

HAVING：
分组后筛选统计结果。


易错点 4：
COUNT(*) 和 COUNT(column_name) 有区别。

COUNT(*)：
统计所有行。

COUNT(column_name)：
统计该列不为 NULL 的行。


易错点 5：
LEFT JOIN 会保留左表所有数据。

例子：

students LEFT JOIN grades

意思是：
所有 students 都会保留。
如果没有成绩，grades 相关列显示 NULL。