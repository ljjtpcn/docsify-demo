?> `create、drop、alter`


### C(Create):创建数据库

```sql
CREATE DATABASE DB3;
```


+ 当要创建的数据库不确定是否存在时

```sql
CREATE DATABASE IF NOT EXISTS DB3; -- 创建DB3前先判断是否存在,不存在则创建
```

+ 指定数据库字符集

```sql
CREATE DATABASE DB4 CHARACTER SET GBK; -- 为新创建的数据库DB4指定字符集为GBK
```

+  将以上两个语法综合使用即为

```sql
CREATE DATABASE IF NOT EXISTS DB3 CHARACTER SET GBK; -- 创建DB4前先判断是否存在,不存在则创建数据库且指定字符集为GBK
```


### R(Retrieve):查询数据库

```sql
SHOW DATABASES;
```

+ 查询某个数据库的默认字符集;查询某个数据库的创建语句

```sql
SHOW CREATE DATABASE DB2;
```

### U(Update):修改数据库

```sql
ALTER DATABASE DB4 CHARACTER SET utf8; -- 修改数据库DB4的字符集为utf8
```

### D(Delete):删除数据库

```sql
DROP DATABASE DB4; -- 删除数据库DB4
```

+ 判断数据库是否存在,存在再删除

```sql
DROP DATABASE IF EXISTS DB4; -- 判断数据库DB4是否存在,存在再删除 注意没有NOT
```

### 使用数据库

+ 查询当前正在使用的数据库名称

```sql
SELECT DATABASE(); -- NULL表示没有使用数据库
```

+ 使用数据库

```sql
USE DB1; -- 使用数据库DB1
```

---

### C(Create):创建表


```sql
CREATE TABLE 表名(
    列名1 数据类型1,
    列名2 数据类型2,
    ...
    列名n 数据类型n
    );
```

> 常用数据类型
> + 整数类型` int`
> + 小数类型 `double(5, 2)`  -- 表示最长5位,小数点后2位(即最大值为999.99)
> + 日期类型 `date` -- 只包含年月日, `yyyy-MM-dd`
> + 日期类型 `datetime`  -- 只包含年月日时分秒, `yyyy-MM-dd HH:mm:ss`
> + 时间戳类型 `timestamp` --  包含年月日时分秒,  如果将来不给这个字段赋值,或赋值为null,则默认自动使用当前的系统时间
> + 字符串类型 `varchar(10)` -- 表示该字段最大10个字符数

+ 例:

```sql
CREATE TABLE student(
	id int,
    name varchar(32),
    age int,
    score double(4, 1),
    birthday date,
    insert_time timestamp
);
```


### R(Retrieve):查询表

+ 查询某个数据库中所有的表名称(当前使用的数据库为`mysql`)

```sql
SHOW TABLES; -- EMPTY表示当前使用的表为空表
```

+ 查询表结构

```sql
DESC host; -- 查询当前mysql数据库中的表host的结构
```

+ 查询表的字符集

```sql
SHOW CREATE TABLE 表名;
```

---


### U(Update):修改表

+ 修改表名 

```sql
ALTER TABLE 表名 RENAME TO 新的表名;
-- 例 -- 
ALTER TABLE student TO stu;
```

+ 修改表的字符集

```sql
ALTER TABLE 表名 CHARACTER SET 字符集名称;
```

+ 添加一列

```sql
ALTER TABLE 表名 ADD 列名 数据类型;
-- 例 --
ALTER TABLE stu ADD gender varchar(10); -- 向表 stu 加入新的列 gender 数据类型为 varchar
```

+ 修改列名称类型 


 ```sql
ALTER TABLE 表名 CHANGE 列名 新列名 新数据类型;
ALTER TABLE 表名 MODIFY 列名 新数据类型;
-- 例 --
ALTER TABLE stu CHANGE gender sex varchar(20); -- 将表stu的gender列重命名为sex,数据类型为varchar(20)
 ```

+ 删除列

```sql
ALTER TABLE 表名 DROP 列名;
```

### D(Delete):删除表

+ 删除

```sql
DROP table 表名; -- 直接删除
```

```sql
DROP table IF EXISTS 表名; -- 先判断是否存在再删除
```

+ 复制表

```sql
CREATE TABLE stu LIKE student; -- 创建一个长得像(LIKE) student 的stu表(即复制了student表)
```

---