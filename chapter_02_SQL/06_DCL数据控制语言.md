# 06_DCL数据控制语言

管理用户：

- 查询用户：`USE mysql;`、`SELEECT * FROM user;`

```sql
CREATE USER 'zl'@'localhost' identified by '123456';
```

- 创建用户：`CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';`

```sql
CREATE USER 'wh'@'%' identified by '123456';
```

- 修改用户密码：`ALTER USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码';`

```sql
ALTER USER 'wh'@'%' IDENTIFIED WITH mysql_native_password by '654321';
```

- 删除用户：`DROP USER '用户名'@'主机名';`

```sql
DROP USER 'zl'@'localhost';
DROP USER 'wh'@'%';
```

> 主机名可以使用%通配。
>
> 这类SQL开发人员较少，主要是DBA (Database Administrator)使用。

权限控制：

|        权限         |        说明        |
| :-----------------: | :----------------: |
| ALL, ALL PRIVILEGES |      所有权限      |
|       SELECT        |      查询数据      |
|       INSERT        |      插入数据      |
|       UPDATE        |      修改数据      |
|       DELETE        |      删除数据      |
|        ALTER        |       修改表       |
|        DROP         | 删除数据库/表/视图 |
|       CREATE        |   创建数据库/表    |

- 查询权限：`SHOW GRANTS FOR '用户名'@'主机名';` 

```sql
SHOW GRANTS FOR 'wh'@'%';
```

- 授予权限：`GRANT 权限列表 ON 数据库.表名 TO '用户名'@'主机名';`

```sql
GRANT ALL ON learn_mysql.* TO 'wh'@'%';
```

- 撤销权限：`REVOKE 权限列表 ON 数据库.表名 FROM '用户名'@'主机名';`

```sql
REVOKE ALL ON learn_mysql.* FROM 'wh'@'%';
```