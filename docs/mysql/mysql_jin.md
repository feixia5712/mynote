### mysql进阶

#### 主键

   PRIMARY KEY 约束

- PRIMARY KEY约束唯一标识数据库表中的每条记录。
- 主键必须包含唯一的值。
- 主键列不能包含 NULL 值。
- 每个表都应该有一个主键，并且每个表只能有一个主键。

实际操作

```
mysql> create table info( id int not null primary key auto_increment, name varchar(30), age int not null, score int not null);
Query OK, 0 rows affected (0.04 sec)

mysql> insert into info(name,age,score) values("张三",18,80);
Query OK, 1 row affected (0.04 sec)

mysql> insert into info(name,age,score) values("zdk",18,90);
Query OK, 1 row affected (0.00 sec)

mysql> insert into info(name,age,score) values("alex",17,70);
Query OK, 1 row affected (0.00 sec)

mysql> insert into info(name,age,score) values("王五",19,70);
Query OK, 1 row affected (0.00 sec)

mysql> select * from info;
+----+--------+-----+-------+
| id | name   | age | score |
+----+--------+-----+-------+
|  1 | 张三   |  18 |    80 |
|  2 | zdk    |  18 |    90 |
|  3 | alex   |  17 |    70 |
|  4 | 王五   |  19 |    70 |
+----+--------+-----+-------+
4 rows in set (0.00 sec)

mysql> desc info
    -> ;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int(11)     | NO   | PRI | NULL    | auto_increment |
| name  | varchar(30) | YES  |     | NULL    |                |
| age   | int(11)     | NO   |     | NULL    |                |
| score | int(11)     | NO   |     | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
4 rows in set (0.00 sec)

mysql> show create table info;
+-------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table | Create Table                                                                                                                                                                                                                      |
+-------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| info  | CREATE TABLE `info` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(30) DEFAULT NULL,
  `age` int(11) NOT NULL,
  `score` int(11) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8 |
+-------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)

```

 我们能看到第四列也就是key那一列，只有id是有PRI，有这个PRI就是表示该字段是表的主键。
 
#### 自增
 
 Auto-increment 会在新记录插入表中时生成一个唯一的数字。

我们通常希望在每次插入新记录时自动创建主键字段的值。我们可以在表中创建一个自动增量（auto-increment）字段。

##### 不设置id字段

```
mysql> create table info( id int not null primary key auto_increment, name varchar(30), age int not null, score int not null);
Query OK, 0 rows affected (0.04 sec)

mysql> insert into info(name,age,score) values("张三",18,80);
Query OK, 1 row affected (0.04 sec)

mysql> insert into info(name,age,score) values("zdk",18,90);
Query OK, 1 row affected (0.00 sec)

mysql> insert into info(name,age,score) values("alex",17,70);
Query OK, 1 row affected (0.00 sec)

mysql> insert into info(name,age,score) values("王五",19,70);
Query OK, 1 row affected (0.00 sec)

mysql> select * from info;
+----+--------+-----+-------+
| id | name   | age | score |
+----+--------+-----+-------+
|  1 | 张三   |  18 |    80 |
|  2 | zdk    |  18 |    90 |
|  3 | alex   |  17 |    70 |
|  4 | 王五   |  19 |    70 |
+----+--------+-----+-------+
4 rows in set (0.00 sec)
mysql> desc info
    -> ;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int(11)     | NO   | PRI | NULL    | auto_increment |
| name  | varchar(30) | YES  |     | NULL    |                |
| age   | int(11)     | NO   |     | NULL    |                |
| score | int(11)     | NO   |     | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
4 rows in set (0.00 sec)

```
 我们能看到第6列也就是Extra那一列，只有id是有auto_increment，有这个auto_increment就是表示该字段是表字段，insert的时候可以不设置。不设置的话，每次步长是根据mysql的配置字段配置。默认是1.
 
##### 修改步长
 
 查看步长
 
 ```
 mysql>  SHOW VARIABLES LIKE 'auto_inc%';
+--------------------------+-------+
| Variable_name            | Value |
+--------------------------+-------+
| auto_increment_increment | 1     |
| auto_increment_offset    | 1     |
+--------------------------+-------+
2 rows in set (0.02 sec)

 ```
 
 配置自增步长，数据表自增将以5为间隔自增。
 
 ```
 mysql> SET @@auto_increment_increment=5;   ### 步长被设置了5，也就是每次插入的数据的时候，都会别前一个id的基础上加上这个步长10
Query OK, 0 rows affected (0.00 sec)

mysql>  SHOW VARIABLES LIKE 'auto_inc%';
+--------------------------+-------+
| Variable_name            | Value |
+--------------------------+-------+
| auto_increment_increment | 5     |
| auto_increment_offset    | 1     |
+--------------------------+-------+
2 rows in set (0.00 sec)

mysql> select * from info;
+----+--------+-----+-------+
| id | name   | age | score |
+----+--------+-----+-------+
|  1 | 张三   |  18 |    80 |
|  2 | zdk    |  18 |    90 |
|  3 | alex   |  17 |    70 |
|  4 | 王五   |  19 |    70 |
+----+--------+-----+-------+
4 rows in set (0.00 sec)

mysql> insert into info(name,age,score) values("kkk",38,89);
Query OK, 1 row affected (0.00 sec)

mysql> select * from info;
+----+--------+-----+-------+
| id | name   | age | score |
+----+--------+-----+-------+
|  1 | 张三   |  18 |    80 |
|  2 | zdk    |  18 |    90 |
|  3 | alex   |  17 |    70 |
|  4 | 王五   |  19 |    70 |
|  6 | kkk    |  38 |    89 |
+----+--------+-----+-------+
5 rows in set (0.00 sec)

mysql> insert into info(name,age,score) values("roort",38,89);
Query OK, 1 row affected (0.00 sec)

mysql> select * from info;
+----+--------+-----+-------+
| id | name   | age | score |
+----+--------+-----+-------+
|  1 | 张三   |  18 |    80 |
|  2 | zdk    |  18 |    90 |
|  3 | alex   |  17 |    70 |
|  4 | 王五   |  19 |    70 |
|  6 | kkk    |  38 |    89 |
| 11 | roort  |  38 |    89 |
+----+--------+-----+-------+
6 rows in set (0.00 sec)

 ```
 
 以上只是临时修改,想要永久修改的话，直接修改配置文件即可(my.cnf)
 
 ```
 增加一句
 
 auto_increment_increment = 12
 ```
 
#### NULL值
 
 基本使用
 
 
- IS NULL：当列的值是NULL，此运算符返回true。
- IS NOT NULL：当列的值不为NULL，运算符返回true。
- <=>： 比较操作符（不同于=运算符），当比较的的两个值为NULL时返回true。

实例操作

```
mysql> use lecy;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> 
mysql> create table llty ( name varchar(30), count int);
Query OK, 0 rows affected (0.04 sec)

mysql> insert into llty (name,count) values('zdk',null);
Query OK, 1 row affected (0.00 sec)

mysql> insert into llty (name,count) values('marry',null);
Query OK, 1 row affected (0.00 sec)

mysql> insert into llty (name,count) values('liy',null);
Query OK, 1 row affected (0.00 sec)

mysql> insert into llty (name,count) values('wangh',89);
Query OK, 1 row affected (0.00 sec)

mysql> insert into llty (name,count) values('zhangdk',65);
Query OK, 1 row affected (0.00 sec)

mysql> select * from llty;
+---------+-------+
| name    | count |
+---------+-------+
| zdk     |  NULL |
| marry   |  NULL |
| liy     |  NULL |
| wangh   |    89 |
| zhangdk |    65 |
+---------+-------+
5 rows in set (0.00 sec)

mysql> desc llty;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| name  | varchar(30) | YES  |     | NULL    |       |
| count | int(11)     | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.01 sec)

mysql>  select * from llty where count=NULL;  #取不出来
Empty set (0.00 sec)

mysql>  select * from llty where count="NULL";  #取不出来
Empty set, 1 warning (0.00 sec)

mysql>  select * from llty where count!="NULL";
+---------+-------+
| name    | count |
+---------+-------+
| wangh   |    89 |
| zhangdk |    65 |
+---------+-------+
2 rows in set, 1 warning (0.00 sec)

mysql>  select * from llty where count!=NULL;
Empty set (0.00 sec)

mysql> select * from llty where count is NULL;
+-------+-------+
| name  | count |
+-------+-------+
| zdk   |  NULL |
| marry |  NULL |
| liy   |  NULL |
+-------+-------+
3 rows in set (0.00 sec)

mysql>  select * from llty where count is not NULL;
+---------+-------+
| name    | count |
+---------+-------+
| wangh   |    89 |
| zhangdk |    65 |
+---------+-------+
2 rows in set (0.00 sec)

mysql> select * from llty where count <=> NULL;
+-------+-------+
| name  | count |
+-------+-------+
| zdk   |  NULL |
| marry |  NULL |
| liy   |  NULL |
+-------+-------+
3 rows in set (0.00 sec)

mysql> 

```
所以当我们想查询null值的时候,最好使用is null 或者 is not null

#### mysql查询正则

MySQL可以通过 LIKE ...% 来进行模糊匹配。

 MySQL 同样也支持其他正则表达式的匹配， MySQL中使用 REGEXP 操作符来进行正则表达式匹配。

 下表中的正则模式可应用于 REGEXP 操作符中。
 
```
 ^ 	匹配输入字符串的开始位置。如果设置了 RegExp 对象的 Multiline 属性，^ 也匹配 '\n' 或 '\r' 之后的位置。
 
 $ 	匹配输入字符串的结束位置。如果设置了RegExp 对象的 Multiline 属性，$ 也匹配 '\n' 或 '\r' 之前的位置。
. 	匹配除 "\n" 之外的任何单个字符。要匹配包括 '\n' 在内的任何字符，请使用象 '[.\n]' 的模式。
[...] 	字符集合。匹配所包含的任意一个字符。例如， '[abc]' 可以匹配 "plain" 中的 'a'。
[^...] 	负值字符集合。匹配未包含的任意字符。例如， '[^abc]' 可以匹配 "plain" 中的'p'。
p1|p2|p3 	匹配 p1 或 p2 或 p3。例如，'z
* 	匹配前面的子表达式零次或多次。例如，zo* 能匹配 "z" 以及 "zoo"。* 等价于{0,}。
+ 	匹配前面的子表达式一次或多次。例如，'zo+' 能匹配 "zo" 以及 "zoo"，但不能匹配 "z"。+ 等价于 {1,}。
{n} 	n 是一个非负整数。匹配确定的 n 次。例如，'o{2}' 不能匹配 "Bob" 中的 'o'，但是能匹配 "food" 中的两个 o。
{n,m} 	m 和 n 均为非负整数，其中n <= m。最少匹配 n 次且最多匹配 m 次。

```
 
 几个简单实例
 
```
 以什么开头
 
 mysql> select * from llty where name regexp '^w';
+-------+-------+
| name  | count |
+-------+-------+
| wangh |    89 |
+-------+-------+
1 row in set (0.01 sec)

范围

mysql> select * from llty where count regexp '[60-90]';
+---------+-------+
| name    | count |
+---------+-------+
| wangh   |    89 |
| zhangdk |    65 |
+---------+-------+
2 rows in set (0.00 sec)

```
 
