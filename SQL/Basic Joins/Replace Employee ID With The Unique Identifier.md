-- 【题目】✅1378. Replace Employee ID With The Unique Identifier(easy)
-- 【链接】https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT unique_id, name
FROM Employees emp
LEFT JOIN EmployeeUNI uni
ON emp.id=uni.id
```

==========================================
Conclusion
==========================================
```text
合并表基本语法：
SELECT column
FROM table1 表1(后面是新名字)
JOIN table2 表2
ON 表1.关联列 = 表2.关联列

left join和right join的区别：
left join保留第一个表的全部列，没有的值补充为null
right join保留第二个表的全部列，没有的值补充为null
```