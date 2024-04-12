# 03_DDL数据定义语言

数据库操作：

- 查询：
  - 查询所有数据库：`SHOW DATABASES;`
  - 查询当前数据库：`SELECT DATABASE();`
- 创建：`CREATE DATABASE [IF NOT EXISTS] 数据库名 [DEFAULT CHARSET 字符集] [COLLATE 排序规则];`
- 删除：`DROP DATABASE [IF EXISTS] 数据库名;`
- 使用：`USE 数据库名;`

表操作：

- 查询：

  - 查询当前数据库所有表：`SHOW TABLES;`
  - 查询表结构：`DESC 表名;`
  - 查询指定表的建表语句：`SHOW CREATE TABLE 表名;`

- 创建：

  ```sql
  CREATE TABLE 表名(
  	字段1 字段1类型 [COMMENT 字段1注释],
      字段2 字段2类型 [COMMENT 字段2注释],
      字段3 字段3类型 [COMMENT 字段3注释],
      ...
      字段n 字段n类型 [COMMENT 字段n注释],
  ) [COMMENT 表注释];
  ```

- 数据类型：

  - 数值类型

  |    类型     |  大小   |        说明        |
  | :---------: | :-----: | :----------------: |
  |  `TINYINT`  | 1 byte  |      小整数值      |
  | `SMALLINT`  | 2 bytes |      大整数值      |
  | `MEDIUMINT` | 3 bytes |      大整数值      |
  |    `INT`    | 4 bytes |      大整数值      |
  |  `BIGINT`   | 8 bytes |     极大整数值     |
  |   `FLOAT`   | 4 bytes |   单精度浮点数值   |
  |  `DOUBLE`   | 8 bytes |   双精度浮点数值   |
  |  `DECIMAL`  |         | 小数值(精确定点数) |

  - 字符串类型

  |     类型     |         大小          |             描述             |
  | :----------: | :-------------------: | :--------------------------: |
  |    `CHAR`    |      0-255 bytes      |          定长字符串          |
  |  `VARCHAR`   |     0-65535 bytes     |          变长字符串          |
  |  `TINYBLOB`  |      0-255 bytes      | 不超过255个字符的二进制数据  |
  |  `TINYTEXT`  |      0-255 bytes      |         短文本字符串         |
  |    `BLOB`    |    0-65 535 bytes     |    二进制形式的长文本数据    |
  |    `TEXT`    |    0-65 535 bytes     |          长文本数据          |
  | `MEDIUMBLOB` |  0-16 777 215 bytes   | 二进制形式的中等长度文本数据 |
  | `MEDIUMTEXT` |  0-16 777 215 bytes   |       中等长度文本数据       |
  |  `LONGBLOB`  | 0-4 294 967 295 bytes |   二进制形式的极大文本数据   |
  |  `LONGTEXT`  | 0-4 294 967 295 bytes |         极大文本数据         |

  - 日期类型

  |    类型     | 大小 |                    范围                    |        格式         |           描述           |
  | :---------: | :--: | :----------------------------------------: | :-----------------: | :----------------------: |
  |   `DATE`    |  3   |         1000-01-01 至  9999-12-31          |     YYYY-MM-DD      |          日期值          |
  |   `TIME`    |  3   |          -838:59:59 至  838:59:59          |      HH:MM:SS       |     时间值或持续时间     |
  |   `YEAR`    |  1   |                1901 至 2155                |        YYYY         |          年份值          |
  | `DATETIME`  |  8   | 1000-01-01 00:00:00 至 9999-12-31 23:59:59 | YYYY-MM-DD HH:MM:SS |     混合日期和时间值     |
  | `TIMESTAMP` |  4   | 1970-01-01 00:00:01 至 2038-01-19 03:14:07 | YYYY-MM-DD HH:MM:SS | 混合日期和时间值，时间戳 |

  ```sql
  /*
  设计一张员工表，要求如下：
      编号 (纯数字)
      工号 (字符串类型，长度不超过10位)
      姓名 (字符串类型，长度不超过10位)
      性别 (存储一个汉字)
      年龄 (不为负数)
      身份证号 (18位)
      入职时间 (取年月日即可)
  */
  
  CREATE TABLE emp(
  	id INT COMMENT '编号',
      workno VARCHAR(10) COMMENT '工号',
      name VARCHAR(10) COMMENT '姓名',
      gender CHAR(1) COMMENT '性别',
      age TINYINT UNSIGNED COMMENT '年龄',
      idno CHAR(18) COMMENT '身份证号',
      entrydate DATE COMMENT '入职时间'
  ) COMMENT '员工表';
  ```

- 修改：

  - 添加字段：`ALTER TABLE 表名 ADD 字段名 类型(长度) [COMMENT 注释] [约束];`

  ```sql
  ALTER TABLE emp ADD nickname VARCHAR(20) COMMENT '昵称';
  ```

  - 修改数据类型：`ALTER TABLE 表名 MODIFY 字段名 新数据类型(长度);`

  ```sql
  ALTER TABLE emp MODIFY nickname VARCHAR(10);
  ```

  - 修改字段名和字段类型：`ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型(长度) [COMMENT 注释] [约束];`

  ```sql
  ALTER TABLE emp CHANGE nickname username VARCHAR(30) COMMENT '用户名';
  ```

  - 删除字段：`ALTER TABLE 表名 DROP 字段名;`

  ```sql
  ALTER TABLE emp DROP username;
  ```

  - 修改表名：`ALTER TABLE 表名 RENAME TO 新表名;`

  ```sql
  ALTER TABLE emp RENAME TO employee;
  ```

- 删除：

  - 删除表：`DROP TABLE [IF EXISTS] 表名;`

  ```sql
  DROP TABLE IF EXISTS tb_user;
  ```

  - 输出指定表，并重新创建该表：`TRUNCATE TABLE 表名;`

  ```sql
  TRUNCATE TABLE tb_user;
  ```

  