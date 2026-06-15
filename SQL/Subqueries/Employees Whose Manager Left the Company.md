-- 【题目】❌1978. Employees Whose Manager Left the Company (Meidum)
-- 【链接】https://leetcode.com/problems/employees-whose-manager-left-the-company

```sql
-- ==========================================
-- Correct solution
-- ==========================================
SELECT employee_id
FROM Employees
Where salary<30000
AND manager_id is not null
AND manager_id not in(
    SELECT employee_id
    FROM Employees
)
ORDER BY employee_id
```

==========================================
Conclusion
==========================================
```text

1.两个条件都会写，但不知道怎么组合。可以用一个判断方法：
先问：这两个条件是要“同时满足”，还是“结果拼在一起”？
如果是“同一个员工同时满足两个条件” → 用 AND
当你需要把两张表或同一张表的两份数据横向拼起来，才用 JOIN。
UNION / UNION ALL 是把两个结果上下拼接。
总结：
| 你想表达             | 用什么                 |
| ------------------- | ------------------- |
| 同一行同时满足两个条件  | `WHERE 条件1 AND 条件2` |
| 满足任意一个条件        | `WHERE 条件1 OR 条件2`  |
| 两个查询结果上下拼接    | `UNION / UNION ALL` |
| 两张表横向匹配信息      | `JOIN`              |
| 一个值是否在另一组结果里 | `IN / NOT IN`       |

```