**对标准的数据进行限定,保证数据的正确性,有效性和完整性。**

### 非空约束

?> NOT NULL **某一列的值不能为`NULL`**

+ 在创建表时添加非空约束

```sql
CREATE TABLE stu(
	id INT,
	name VARCHAR(20) NOT NULL -- name为非空
);
```
+ 在表创建完后添加`name`的非空约束

```sql
ALTER TABLE stu MODIFY name VARCHAR(20) NOT NULL;
```
+ 删除`name`的非空约束

```sql
ALTER TABLE stu MODIFY name VARCHAR(20);
```

### 唯一约束(唯一索引)
?> UNIQUE **某一列的值不能重复**

+ 在创建表时添加唯一约束

```sql
CREATE TABLE stu(
	id INT,
	phone VARCHAR(20) UNIQUE -- 手机号不能重复
);
```
+ 在表创建完后添加`phone`的唯一约束

```sql
ALTER TABLE stu MODIFY phone VARCHAR(20) UNIQUE;
```
+ 删除`phone`的唯一约束

```sql
-- ALTER TABLE 表名 DROP INDEX 索引名;
ALTER TABLE stu DROP INDEX phone; -- 删除唯一约束(与非空约束删除语法不一样)
```
!> 唯一约束可以有`NULL`值, 但是只能有一条记录为`NULL`值


### 主键约束
?> PRIMARY KEY **非空且唯一**

+ 在创建表时添加主键约束

```sql
CREATE TABLE stu(
	id INT PRIMARY KEY, -- 给id添加主键约束
	name VARCHAR(20)
);
```

+ 在表创建完后添加`id`的主键约束

```sql
ALTER TABLE stu MODIFY id INT PRIMARY KEY;
```


+ 删除`id`的主键约束

```sql
ALTER TABLE stu DROP PRIMARY KEY;  -- 删除主键约束(与前面约束删除语法不一样)
```

!> 1. 一张表中只能有一个字段为主键</br>
2. 主键就是表中记录的唯一标识  

### 自动增长
?> 如果某一列是数值类型,使用 `auto_increment` 可以完成自动增长,一般配合主键约束使用

+ 在创建表时添加主键约束,完成自动增长

```sql
CREATE TABLE stu(
	id INT PRIMARY KEY AUTO_INCREMENT, -- 给id添加主键约束,完成自动增长
	NAME VARCHAR(20)
);
```


+ 删除自动增长

```sql
ALTER TABLE stu MODIFY id INT;
```


+ 添加自动增长

```sql
ALTER TABLE stu MODIFY id INT AUTO_INCREMENT;
```

### 外键约束
?> FOREIGN KEY 让表与表产生关系, 从而保证数据的正确性

+ 在创建表时添加外键

```sql
CREATE TABLE 表名(
	......
	外键列
	CONSTRAINT 外键名称 FOREIGN KEY (外键列名称) REFERENCES 主表表名(主表列名称);
);
```

+ 在表创建完后添加外键

```sql
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键列名称) REFERENCES 主表表名(主表列名称);
```


+ 删除外键

```sql
ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
```
+ 例

```sql
CREATE TABLE class(
	id INT PRIMARY KEY AUTO_INCREMENT,
	username VARCHAR(20),
);

CREATE TABLE student(
	id INT PRIMARY KEY AUTO_INCREMENT,
	NAME VARCHAR(20),
	age INT,
	class_id INT, -- 外键对应主表的主键
	CONSTRAINT stu_class_fk FOREIGN KEY (class_id) REFERENCES class(id)
);
```
!> `class`表必须先创建, 即被关联的表必须先创建才能被关联
~~先有爸爸后有儿子~~,外键可以为`null`但是不能为不存在的值

---

### 级联更新

+ 在表创建完后添加外键,设置级联更新

```sql
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键列名称) REFERENCES 主表表名(主表列名称) ON UPDATE CASCADE;
```

### 级联删除
+ 在表创建完后添加外键,设置级联删除

```sql
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键列名称) REFERENCES 主表表名(主表列名称) ON DELETE CASCADE;
```
!> **级联更新**为ON `UPDATE` CASCADE</br>
   **级联删除**为ON `DELETE` CASCADE