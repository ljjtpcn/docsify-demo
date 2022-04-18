**DBA：数据库管理员**

### 管理用户

1. 添加用户

```sql
CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';
```

2. 删除用户

```sql
DROP USER '用户名'@'主机名';
```

3. 修改用户密码

```sql
---PASSWORD()为加密函数
UPDATE USER SET PASSWORD = PASSWORD('新密码') WHERE USER = '用户名';
--例
UPDATE USER SET PASSWORD = PASSWORD('abcd') WHERE USER = 'lisi';

SET PASSWORD FOR '用户名'@'主机名' = PASSWORD('新密码');
--例
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('123');
```

4. 查询用户

```sql
-- 1. 切换到mysql数据库
USE myql;
-- 2. 查询user表
SELECT * FROM USER;
```
> 通配符： % 表示可以在任意主机使用用户登录数据库
### 权限管理
1. 查询权限

```sql
-- 查询权限
SHOW GRANTS FOR '用户名'@'主机名';
-- 例
SHOW GRANTS FOR 'lisi'@'%';
```
2. 授予权限

```sql
-- 授予权限
GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';

-- 给张三用户授予查询, 修改权限，在任意数据库任意表上
GRANT SELECT,UPDATE ON *.* TO 'zhangsan'@'localhost';

-- 给张三用户授予创建权限，在任意数据库任意表上（注意授予创建权限时不加 ON！！！）
GRANT CREATE TO 'zhangsan'@'localhost';

-- 给张三用户授予所有权限，在任意数据库任意表上
GRANT ALL ON *.* TO 'zhangsan'@'localhost';
```
3. 撤销权限

```sql
-- 撤销权限
REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';
REVOKE UPDATE ON db3.`account` FROM 'lisi'@'%';
```