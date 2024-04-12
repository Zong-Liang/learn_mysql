# 05_DQL数据查询语言

语法：

```sql
SELECT
	字段列表
FROM
	表名列表
WHERE
	条件列表
GROUP BY
	分组字段列表
HAVING
	分组后条件列表
ORDER BY
	排序字段列表
LIMIT
	分页参数
```

基本查询：

- 查询多个字段：`SELECT 字段1, 字段2,... FROM 表名;`、`SELECT * FROM 表名;`

```sql
SELECT name,workno,age FROM emp;

SELECT id, workno, name, gender, age, idcard, workaddress, entrydate FROM emp;

SELECT * FROM emp;
```

- 设置别名：`SELECT 字段1 [AS 别名1], 字段2 [AS 别名2],... FROM 表名;`

```sql
SELECT workaddress AS '工作地址' FROM emp;

SELECT workaddress '工作地址' FROM emp;
```

- 去除重复记录：`SELECT DISTINCT 字段1, 字段2,... FROM 表名;`

```sql
SELECT DISTINCT workaddress '工作地址' FROM emp;
```

条件查询 (`WHERE`)：`SELECT 字段1, 字段2,... FROM 表名 WHERE 条件列表;`

|      运算符      |              功能              |
| :--------------: | :----------------------------: |
|        >         |              大于              |
|        >=        |            大于等于            |
|        <         |              小于              |
|        <=        |            小于等于            |
|        =         |              等于              |
|      <>或!=      |             不等于             |
| BETWEEN...AND... |         在某个范围之内         |
|     IN(...)      | 在IN之后列表中的多个值中选一个 |
|   LIKE 占位符    |            模糊匹配            |
|  IS (NOT) NULL   |           是否为NULL           |
|    AND 或 &&     |              并且              |
|    OR 或 \|\|    |              或者              |
|     NOT 或 !     |               非               |

```sql
SELECT * FROM emp WHERE age = 10;

SELECT * FROM emp WHERE age < 10;

SELECT * FROM emp WHERE age <= 10;

SELECT * FROM emp WHERE idcard IS NULL;

SELECT * FROM emp WHERE idcard IS NOT NULL;

SELECT * FROM emp WHERE age != 10;
SELECT * FROM emp WHERE age <> 10;

SELECT * FROM emp WHERE age = 10 && id > 5;
SELECT * FROM emp WHERE age = 10 AND id > 10;

SELECT * FROM emp WHERE age BETWEEN 6 AND 12;

SELECT * FROM emp WHERE gender = '女' AND id > 10;

SELECT * FROM emp WHERE age = 10 OR age = 20 OR age = 30;
SELECT * FROM emp WHERE age IN (10,20,30);

SELECT * FROM emp WHERE name LIKE '___';

SELECT * FROM emp WHERE idcard LIKE '%X';
SELECT * FROM emp WHERE idcard LIKE '_________________X';
```

聚合函数：`SELECT 聚合函数(字段1, 字段2,...) FROM 表名`，将一列数据作为一个整体进行纵向计算。

|  函数   |   功能   |
| :-----: | :------: |
| `COUNT` | 统计数量 |
|  `MAX`  |  最大值  |
|  `MIN`  |  最小值  |
|  `AVG`  |   均值   |
|  `SUM`  |   求和   |

```sql
SELECT COUNT(*) FROM emp;

SELECT COUNT(id) FROM emp;

SELECT AVG(age) FROM emp;

SELECT MAX(age) FROM emp;

SELECT MIN(age) FROM emp;

SELECT SUM(age) FROM emp WHERE workaddress='北京';
```

> NULL值不参与聚合函数计算。

分组查询 (`GROUP BY`)：`SELECT 字段1, 字段2,... FROM 表名 [WHERE 条件] GROUP BY 分组字段 [HAVING 分组过滤条件];`

```sql
SELECT gender, COUNT(*) FROM emp GROUP BY gender;

SELECT gender, AVG(age) FROM emp GROUP BY gender;

SELECT workaddress, COUNT(*) FROM emp WHERE age < 20 GROUP BY workaddress HAVING COUNT(*) >= 3;
```

> WHERE和HAVING的区别：
>
> - 执行时机不同：WHERE是分组前过滤，不满足条件不参与分组，HAVING是分组之后对结果进行过滤。
> - 判断条件不同：WHERE不能对聚合函数进行判断，而HAVING可以。

排序查询 (`ORDER BY`)：`SELECT 字段1, 字段2,... FROM 表名 ORDER BY 字段1 排序方式1, 字段2 排序方式2,... ` 

```sql
SELECT * FROM emp ORDER BY age asc;
SELECT * FROM emp ORDER BY age;
SELECT * FROM emp ORDER BY age desc;

SELECT * FROM emp ORDER BY entrydate desc;

SELECT * FROM emp ORDER BY age, entrydate desc;
```

分页查询 (`LIMIT`)：`SELECT 字段1, 字段2,... FROM 表名 LIMIT 起始索引, 查询记录数;`

```sql
SELECT * FROM emp LIMIT 0, 5;
SELECT * FROM emp LIMIT 10;

SELECT * FROM emp LIMIT 5, 5;
```

> 起始索引从0开始，起始索引=(查询页码-1)*每页显示记录数。
>
> 分页查询是数据库的方言，不同数据库有不同实现方式。
>
> 如果查询的是第一页的数据，起始索引可以省略，直接简写为`LIMIT 10;`

执行顺序：

```sql
SELECT          ④
	字段列表
FROM            ①
	表名列表
WHERE           ②
	条件列表
GROUP BY        ③
	分组字段列表
HAVING
	分组后条件列表
ORDER BY        ⑤
	排序字段列表
LIMIT           ⑥
	分页参数
```

