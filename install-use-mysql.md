---
title: MySQL 的安装和基本指令
---
## 安装

### 安装 MySQL 服务端,核心程序

`sudo apt-get install mysql-server`

### 安装 MySQL 客户端

`sudo apt-get isntall mysql-client`

### 安装结束以后,使用命令验证是否安装并且启动成功

`sudo netstat -tap | grep mysql`

### 可以根据自己的需求，修改 MySQL 的配置文件（my.cnf）,使用以下命令

`sudo vim /etc/mysql/my.cnf`

## 简单使用

### 打开 MySQL

```
# 启动 MySQL 服务
sudo service mysql start

# 使用 root 用户登录
mysql -u root
```

### 查看数据库

`show databases;`

### 连接数据库

`use information_schema`

### 查看表

`show tables;`

### 退出

`quit 或者 exit`

### 新建数据库

`CREATE DATABASE <数据库名字>`

### 在数据库中新建一个表

```
CREATE TABLE <表的名字>
(
列名a 数据类型(数据长度)<选填:PRIMARY KEY>,
列名b 数据类型(数据长度)<选填:DEFAULT '<默认值>'>，
列名c 数据类型(数据长度) NOT NULL,
列名d int auto_increment,
PRIMARY KEY(<列名>),
UNIQUE(<列名>),
)
```

### 创建关联

```
# 创建表的时候进行添加
constraint symbol foreign key(本表列名) references <关联表名>(关联列名);
# 已经创建好的表进行添加
ALTER TABLE <表名> ADD FOREIGN KEY(本表列名) REFERENCES <关联表名>(关联列名);
```

### 向表中插入数据

`INSERT INTO <表的名字>(列名a,列名b,列名c) VALUES(值1,值2,值3);`

### 删除数据库

`DROP DATABASE <数据库名字>`

### 删除表

`DROP TABLE <表的名字>`

### 加载 sql 文件

`source <路径和文件名>`

## SQL 约束

主键(PRIMARY KEY)不能有重复,并且不能为空

默认值(DEFAULT)当插入数据为空时,将使用默认值

唯一值(UNIQUE)指定的列不能有重复的值,如果插入数据时重复,则插入数据失败

外键 (FOREIGN KEY) 既能确保数据完整性，也能表现表之间的关系,一个表可以有多个外键，每个外键必须 REFERENCES (参考) 另一个表的主键，被外键约束的列，取值必须在它参考的列中有对应值

非空(NOT NULL)被非空约束的列，在插入值时必须非空,如果为空,会被警告,但是插入数据成功(5.5版本),禁止插入数据(5.6版本以上)

## SELECT语句详解

### 基本的SELECT语句

基本格式 :

`SELECT 要查询的列名 FROM 表名字 WHERE 限制条件;`

### 数学符号条件

SELECT 语句经常使用 WHERE 限制条件

数学符号限制 : =, <, >, <=, >=

`SELECT name,age FROM employee WHERE age>25;`

### 逻辑关系

可以使用 AND 和 OR :

`SELECT name,age FROM employee WHERE age<25 OR age>30;`

```
# 筛选出 age 大于 25，且 age 小于 30
SELECT name,age FROM employee WHERE age>25 AND age<30;
# 如果需要包含25和30这两个数字的话，可以替换为 **age BETWEEN 25 AND 30**
```

### IN 和 NOT IN

使用 In 和 NOT IN 筛选在不在某个范围内

`SELECT name,age,phone,in_dpt FROM employee WHERE in_dpt IN ('dpt3','dpt4');`

### 通配符

LIKE在SQL语句中和通配符一起使用 `_`代表一个未指定字符,'%'代表不定量个未指定字符

`SELECT name,age,phone FROM employee WHERE phone LIKE '1101__';`

### 对结果进行排序

关键词`ORDER BY` 默认是升序排列,`ASC`指定升序,'DESC'指定降序

`SELECT name,age,salary,phone FROM employee ORDER BY salary DESC;`

### 内置函数和计算

函数名：	|COUNT	|SUM	|AVG	|MAX	|MIN
---|---|---|---|---|---
作用：	|计数	|求和	|求平均值	|最大值	|最小值

AS 关键词可以给值重命名

`SELECT MAX(salary) AS max_salary,MIN(salary) FROM employee;`

### 子查询

查询Tom所在部门做了几个工程.Tom在employee表,工程在project表.所查询的内容都来自一个表,这个时候可以使用子查询

`SELECT of_dpt,COUNT(proj_name) AS count_project FROM project
WHERE of_dpt IN
(SELECT in_dpt FROM employee WHERE name='Tom');`

### 连接查询

当处理多个表,并且结果来自不同的表的时候,使用 JOIN 操作,把多个表当作一个新的表进行操作

`SELECT id,name,people_num
FROM employee,department
WHERE employee.in_dpt = department.dpt_name
ORDER BY id;`

或者使用 JOIN ON 语法

`SELECT id,name,people_num
FROM employee JOIN department
ON employee.in_dpt = department.dpt_name
ORDER BY id;`

`GROUP BY` 使用某一列的值作为唯一值进行组合,相同的项会被组合到一块

```
inner join是指
select * from a inner join b on a.aid = b.bid仅取出a,b匹配的数据

left join 指:
select * from a left join b on a.aid = b.bid
首先取出a表中所有数据,然后再加上与a,b匹配的的数据

right join
指的是首先取出b表中所有数据,然后再加上与a,b匹配的的数据
```

## 数据库和表的修改和删除

### 对数据库的修改

删除数据库

`DROP DATABASE <数据库名>;`

### 对一张表的修改

重命名一张表,三种命令格式

```
RENAME TABLE 原名 TO 新名字;
ALTER TABLE 原名 RENAME 新名;
ALTER TABLE 原名 RENAME TO 新名;
```

删除一张表

`DROP TABLE <表名字>;`

### 对一列的修改(对表结构的修改)

增加一列

```
ALTER TABLE 表名字 ADD COLUMN 列名字 数据类型 约束;

或： ALTER TABLE 表名字 ADD 列名字 数据类型 约束;

# 将新的列放在某一列的后面,使用关键词 AFTER

ALTER TABLE 表名字 ADD COLUMN <新列名字> 数据类型 约束 **AFTER** <某一列>;

放在第一列,在最后使用关键词 **FIRST**
```

删除一列,将 ADD 改为 DROP

```
ALTER TABLE 表名字 DROP COLUMN 列名字;

或： ALTER TABLE 表名字 DROP 列名字;
```

重命名一列(修改一列),当原列名和新列名相同时,则只修改数据类型或约束或者位置

`ALTER TABLE 表名字 CHANGE 原列名 新列名 数据类型 约束;`

修改数据类型

`ALTER TABLE 表名字 MODIFY 列名字 新数据类型;`

### 对表的内容修改

修改表中的某个值

`UPDATE 表名字 SET 列1=值1,列2=值2 WHERE 条件;`

删除一行记录

`DELETE FROM 表名字 WHERE 条件;`
