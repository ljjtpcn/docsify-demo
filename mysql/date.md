### 查询

+ 根据日期段查询数据

```sql
-- 获取一天内的数据
select * FROM 数据表  WHERE  DATE_SUB(CURDATE(), INTERVAL 1 DAY) <= 时间字段名;
-- 获取一周内的数据
select * FROM 数据表  WHERE  DATE_SUB(CURDATE(), INTERVAL 1 WEEK) <= 时间字段名;
-- 获取一月内的数据
SELECT * FROM 数据表  WHERE  DATE_SUB(CURDATE(), INTERVAL 1 MONTH) <=  时间字段名;
-- 获取一年内的数据
SELECT * FROM 数据表  WHERE  DATE_SUB(CURDATE(), INTERVAL 1 YEAR) <=  时间字段名;
```

> 注意：如果数据库中时间以UNIX时间戳的形式存放，在时间对比上需要更改为统一格式: `DATE_SUB()`返回的是格式化后的时间：2014-05-17
需要用`UNIX_TIMESTAMP()`转化为UNIX时间戳形式对比如:
```sql
-- 获取一天内的数据
select * FROM 数据表  WHERE  UNIX_TIMESTAMP(DATE_SUB(CURDATE(), INTERVAL 1 DAY)) <= 时间字段名;
