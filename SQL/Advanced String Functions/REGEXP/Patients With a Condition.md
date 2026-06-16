-- 【题目】✅1527. Patients With a Condition(Easy)
-- 【链接】https://leetcode.com/problems/patients-with-a-condition

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT patient_id,patient_name,conditions
FROM Patients
WHERE conditions LIKE 'DIAB1%'
OR    conditions LIKE '% DIAB1%'
```

==========================================
Conclusion
==========================================
```text
LIKE用法
```