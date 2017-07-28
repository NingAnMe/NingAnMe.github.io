# 安装

### 安装 MySQL 服务端,核心程序

`sudo apt-get install mysql-server`

### 安装 MySQL 客户端

`sudo apt-get isntall mysql-client`

### 安装结束以后,使用命令验证是否安装并且启动成功

`sudo netstat -tap | grep mysql`

### 可以根据自己的需求，修改 MySQL 的配置文件（my.cnf）,使用以下命令

`sudo vim /etc/mysql/my.cnf`

# 简单使用

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

# 深入使用

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

# SQL 约束

主键(PRIMARY KEY)不能有重复,并且不能为空

默认值(DEFAULT)当插入数据为空时,将使用默认值

唯一值(UNIQUE)指定的列不能有重复的值,如果插入数据时重复,则插入数据失败

外键 (FOREIGN KEY) 既能确保数据完整性，也能表现表之间的关系,一个表可以有多个外键，每个外键必须 REFERENCES (参考) 另一个表的主键，被外键约束的列，取值必须在它参考的列中有对应值

非空(NOT NULL)被非空约束的列，在插入值时必须非空,如果为空,会被警告,但是插入数据成功(5.5版本),禁止插入数据(5.6版本以上)




