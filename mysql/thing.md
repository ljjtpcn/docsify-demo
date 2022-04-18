### 事务的基本介绍
> 如果一个包含多个步骤的业务操作，被事务管理，那么这些操作要么同时成功，要么同时失败。

+ 操作: 

```sql
1. 开启事务: start transaction;
2. 回滚: rollback; -- 出现异常回滚
3. 提交: commit; -- 正常提交
```
+ 事务提交的两种方式(**MySQL**数据库中事务默认自动提交)
  + 自动提交：

      一条DML(增删改)语句会自动提交一次事务。

  + 手动提交：

      **Oracle** 数据库默认是手动提交事务(需要先开启事务，再提交)

+ 查看事务的默认提交方式

```sql
SELECT @@autocommit; -- 1 代表自动提交  0 代表手动提交
```
 + 修改默认提交方式

```sql
SET @@autocommit = 0; -- 1 代表自动提交  0 代表手动提交 
```

### **事务的四大特征**
	1. 原子性：是不可分割的最小操作单位，要么同时成功，要么同时失败。
	2. 持久性：当事务提交或回滚后，数据库会持久化的保存数据。
	3. 隔离性：多个事务之间,相互独立。
	4. 一致性：事务操作前后，数据总量不变



### 事务的隔离级别(了解)

* 概念：多个事务之间隔离的，相互独立的。但是如果多个事务操作同一批数据，则会引发一些问题，设置不同的隔离级别就可以解决这些问题。
	* 存在问题：
		1. 脏读：一个事务，读取到另一个事务中没有提交的数据
		2. 不可重复读(虚读)：在同一个事务中，两次读取到的数据不一样。
		3. 幻读：一个事务操作(DML)数据表中所有记录，另一个事务添加了一条数据，则第一个事务查询不到自己的修改。
	* 隔离级别：
		1. `read uncommitted`：读未提交
			* 产生的问题：脏读、不可重复读、幻读
		2. `read committed`：读已提交 （Oracle）
			* 产生的问题：不可重复读、幻读
		3. `repeatable read`：可重复读 （MySQL默认）
			* 产生的问题：幻读
		4. `serializable`：串行化
			* 可以解决所有的问题

		>隔离级别从小到大安全性越来越高，但是效率越来越低
	* 数据库查询隔离级别：
		`select @@tx_isolation;`
	* 数据库设置隔离级别：
        `set global transaction isolation level  级别字符串;`

+ 演示

```sql
set global transaction isolation level read uncommitted;
start transaction;
-- 转账操作
update account set balance = balance - 500 where id = 1;
update account set balance = balance + 500 where id = 2;
```