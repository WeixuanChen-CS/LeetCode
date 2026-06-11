-- 【题目】✅1070. Product Sales Analysis III(Medium)
-- 【链接】https://leetcode.com/problems/product-sales-analysis-iii/

```sql
-- ==========================================
-- My solution
-- ==========================================
SELECT tweet_id
FROM Tweets
WHERE length(content)>15
```

==========================================
Conclusion
==========================================
```text
如果你想计算某列里有多少个字符/字母，常用语法是：
LENGTH(content)
如果计算的包含非字节：
CHAR_LENGTH(content)
```
