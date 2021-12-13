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