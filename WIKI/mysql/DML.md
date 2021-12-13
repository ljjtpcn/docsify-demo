
?> `insert、update、delete`


### 添加数据

```sql
INSERT INTO 表名(列名1, 列名2, ...,列名n) VALUES(值1, 值2, ..., 值n);
-- 例 --
INSERT INTO student(id, name, age) VALUES(1, 'ljj', 21);
```

> 列名和值要一一对应
>
> 如果表名后不给定列名, 则默认给所有列添加值
>
> ​ `INSERT INTO 表名 VALUES(值1, 值2, ..., 值n);`
>
> 除了数字类型,其他类型需要使用引号(单双均可)引起来

### 删除数据

```sql
DELETE FROM 表名 [WHERE 条件];
-- 例 --
DELETE FROM student WHERE id = 1; -- 从表student中删除id值为1的数据
```

> 如果不加`WHERE`条件,则删除表中所有数据
>
> 如果要删除所有记录
>
>    + `DELETE FROM 表名;` -- 不推荐使用。有多少条记录就会执行多少次删除操作,效率低
>    + `TRUNCATE TABLE 表名;` -- 推荐使用。先删除表然后再创建一张一模一样的空表，效率高

### 修改数据

```sql
UPDATE 表名 SET 列名1 = 值1, 列名2 = 值2 [WHERE id = 1];
-- 例 --
UPDATE student SET age = 110, score = 100 WHERE id = 1;
```

!> 如果不加任何条件, 则会将表中所有记录全部修改

---