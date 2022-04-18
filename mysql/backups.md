### 命令行

备份:

`mysqldump -u用户名 -p密码 数据库名称 > 保存的路径(如D://back.sql)`

还原:

**1. [登录数据库](mysql/login.md)**
```bash
mysql -h ip -P 3306 -u 用户名 -p密码
```

**2. [创建数据库](mysql/DDL.md)**

```sql
CREATE DATABASE db1;
```
**3. 使用数据库**
```sql
USE db1;
```

**4. 执行备份文件**
```sql
source D://back.sql
```

