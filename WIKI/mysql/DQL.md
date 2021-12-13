?> `select`


```sql
SELECT
	字段列表
FROM
	表名列表
WHERE
	条件列表
GROUP BY
	分组列表
HAVING
	分组之后的条件
ORDER BY
	排序
LIMIT
	分页限定
```

### 多个字段的查询

```sql
-- 查询多个字段 --
SELECT name, age FROM student;
-- 也可以查询单个字段 --
SELECT address FROM student;
-- 查询所有字段 --
SELECT * FROM student; -- 工作中一般不让用
```

### 去除重复结果集

上一步我们查询了`address`发现有重复的地址(香港),有没有办法去除呢?~~(我寻思这不是废话吗!当然有)~~

```sql
SELECT DISTINCT address FROM student; -- 这里去除的是address上的重复
SELECT DISTINCT name, address FROM student; -- 这里去除的是name字段和address字段同时相同时的重复
```

### 计算列

```sql
-- 一般可以使用四则运算计算一些列的值(一般只会进行数字型的计算)
/* 计算 math 和 english 之和
   注意 如果有null 参与的运算,那么计算结果都为 null
   IFNULL(english, 0) 表示如果english为null则替换成0进行计算
*/
SELECT name, math, english, math + IFNULL(english, 0) FROM student;
```

### 起别名

~~有没有发现上面计算的`math+english`列很长,很难看~~ ,所以接下来我们可以给该列取个别名

```sql
SELECT name, math, english, math + IFNULL(english, 0) AS 总分 FROM student; -- AS 总分
```

`AS`都可以省略,但是要用**空格**代替

```sql
SELECT name 姓名, math 数学, english 英语, math + IFNULL(english, 0)  总分 FROM student; -- 空格代替AS
```

### 条件查询
```sql
-- 查询年龄在20~30之间的数据
SELECT * FROM student WHERE age < 30 AND age > 20;
SELECT * FROM student WHERE age BETWEEN 20 AND 30;
-- 查询年龄是19或者22或者25的数据
SELECT * FROM student WHERE age = 19 OR age = 22 OR age = 25;
SELECT * FROM student WHERE age IN(19,22,25);
-- 查询english为NULL或者不为NULL的数据
SELECT * FROM student WHERE english = NULL; -- 错误语法
SELECT * FROM student WHERE english IS NULL; -- 正确语法
SELECT * FROM student WHERE english IS NOT NULL; -- 正确语法
```

!> 对于`NULL`值的查询不能使用`=`或者`!=`, 而应当使用`IS`或者`IS NOT`

### 模糊查询

`%`: 匹配多个(可以是0个)字符

`_`: 匹配单个字符

```sql
-- 查询姓马的人
SELECT * FROM student WHERE NAME LIKE '马%';
-- 查询姓马且名字为2个字的人
SELECT * FROM student WHERE NAME LIKE '马_';
-- 查询姓名第二个字是化的人
SELECT * FROM student WHERE NAME LIKE '_化%';
-- 查询姓名中包含马的人
SELECT * FROM student WHERE NAME LIKE '%马%';
```

### 排序查询

?> 根据某些字段进行升序或降序排列

**语法: ORDER BY 排序字段1, 排序方式1, 排序字段2, 排序方式2, ...;**

```sql
SELECT * FROM student ORDER BY math; -- 默认为ASC升序排序
SELECT * FROM student ORDER BY math DESC; -- DESC降序排序
-- 先按math升序排序,当math一样时,则使用english升序排序
SELECT * FROM student ORDER BY math ASC, english ASC; 
```

### 聚合函数

?> 将某一列数据作为一个整体,进行纵向的计算

1. `count`: 计算个数
2. `max(min)`: 取最大(最小)值
3. `sum`: 计算和
4. `avg`: 计算平均值

```sql
SELECT COUNT(NAME) FROM student; -- 一般选择主键进行计算,不推荐使用 count(*)
SELECT MIN(IFNULL(english, 0)) FROM student;
SELECT AVG(IFNULL(english, 0)) FROM student;
```

!> 聚合函数的计算排除了`NULL`值,如需加上`NULL`,可使用`IFNULL`语法或选择不包含`NULL`的列进行计算

### 分组查询

?> 以某一字段为依据进行分组,再进行各种查询

**语法: GROUP BY 分组字段;**

```sql
--按照性别分组,分别查询男女同学的平均分, 人数
SELECT sex, AVG(IFNULL(english, 0)), COUNT(id) FROM student GROUP BY sex;
-- 以下查询字段中包含了name字段,语法虽然不会报错,但是是无意义的
SELECT name, sex, AVG(IFNULL(english, 0)) FROM student GROUP BY sex;
-- 在分组之前可以添加WHERE条件限制参加分组的数据,如以下是仅数学分数大于70的同学才能参加分组
SELECT sex, AVG(IFNULL(math, 0)), COUNT(id) 人数 FROM student WHERE math > 70 GROUP BY sex;
--按照性别分组,分别查询男女同学的平均分, 人数, 要求:数学大于70分的人才参与分组,分组之后人数应大于2人
SELECT sex, AVG(IFNULL(math, 0)), COUNT(id) 人数 FROM student WHERE math > 70 GROUP BY sex HAVING 人数 > 2;
```

!> 1. 分组查询的字段应为分组字段或者聚合函数,不要使用此之外的字段,因为那是毫无意义的</br>
2. 在**分组之前**可以使用`WHERE`条件限制参加分组的数据</br>
3. 在**分组之后**可以使用`HAVING`条件限制需要查询的分组的数据

`WHERE`和`HAVING`的区别?

1. `WHERE`在分组之前进行限定,如果不满足条件,则不参与分组。`HAVING`在分组之后进行限定,如果不满足结果, 则不会被查询出来
2. `WHERE`后不可以跟聚合函数, `HAVING`可以进行聚合函数的判断


### 分页查询

?> 分页显示查询结果

**语法: LIMIT 开始的索引, 每页查询的条数;**

```sql
-- 每页显示3条
SELECT * FROM student LIMIT 0, 3; -- 第一页
SELECT * FROM student LIMIT 3, 3; -- 第二页

-- 公式: 开始的页码 = (当前的页码 - 1) * 每页显示的条数
```

!> `LIMIT`为MySQL的**方言**