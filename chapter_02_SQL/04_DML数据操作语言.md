# 04_DML数据操作语言

添加数据 (`INSERT`)：

- 给指定字段添加数据：`INSERT INTO 表名 (字段名1, 字段名2,...) VALUES (值1, 值2,...);`

```sql
INSERT INTO employee(id, workno, name, gender, age, idno, entrydate) VALUES (1,'1','zl','男',10,'123456789012345678','2000-01-01');
```

- 给全部字段添加数据：`INSERT INTO 表名 VALUES (值1, 值2,...);`

```sql
INSERT INTO employee VALUES (2,'2','wh','女',18,'123456780123456789','2001-02-02');
```

- 批量添加数据：`INSERT INTO 表名 (字段名1, 字段名2,...) VALUES (值1, 值2,...), (值1, 值2,...),...;`、`INSERT INTO 表名 VALUES (值1, 值2,...), (值1, 值2,...),...;`

```sql
INSERT INTO employee VALUES (3,'3','zs','女',15,'123456780123456789','2001-02-03'),(4,'4','ls','男',16,'123453456789678012','2001-04-03');
```

> 插入数据时，指定的字段顺序需要与值的顺序一一对应。
>
> 字符串和日期类型数据应该包含在引号中。
>
> 插入数据的大小应该在字段的指定范围内。

修改数据 (`UPDATE`)：`UPDATE 表名 VALUES 字段名1=值1, 字段名2=值2,...[WHERE 条件];`

```sql
UPDATE employee SET name='ww' WHERE id=1;

UPDATE employee SET name='mm',gender='女' WHERE id=1;

UPDATE employee SET entrydate='2008-01-01';
```

> 修改语句的条件没有的话就是修改整张表的所有数据。

删除数据 (`DELETE`)：`DELETE FROM 表名 [WHERE 条件];`

```sql
DELETE FROM employee WHERE gender='女';

DELETE FROM employee;
```

> 删除语句的条件如果没有则会删除整张表的所有数据。
>
> 删除语句不能删除某一个字段的值，这个操作可以使用修改语句来实现。
