### 登录数据库
```bash
mysql -h ip -P 3306 -u 用户名 -p密码
```

+ `-h`表示host,即主机的ip地址
+ `-P`表示port(端口)，mysql数据库的默认端口是3 306,你可以自己改端口号(注意：这是大写的字母P)
+ `-u`表示user用户名
+ `-p`表示password密码(注意：这是小写的字母p),大写的P表示端口号，小写的p表示密码
+ 小写的p表示密码，`-p`和密码之间不能有空格,其他 `-u，-h，-P`之类的，是可以有空格的，也可以没有空 格

!> 如果是本机，主机ip和端口号可以不写(即主机ip和端+口号可以省略)，直接写成mysql -u 用户名 -p密码。
</br>
如果是本机，但是端口号改成了其他的端口号，不是默认的3306了，比如将端口号改成了6688，登录时就加上端口号，即mysql -P 6688 -u 用户名 -p密码。
