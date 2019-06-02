### 多表查询

#### 介绍

主要包含三种:
- 多表连接查询
- 复合条件连接查询
- 子查询

创建表

```
mysql> create table department(
    -> id int,
    -> name varchar(30)
    -> );
Query OK, 0 rows affected (0.03 sec)

mysql> create table employee(
    -> id int primary key auto_increment,
    -> name varchar(20),
    -> sex enum('male','female') not null default 'male',
    -> age int,
    -> dep_id int);
Query OK, 0 rows affected (0.02 sec)

mysql> insert into department values(200,'技术');
Query OK, 1 row affected (0.00 sec)

mysql> insert into department values(300,'销售');
Query OK, 1 row affected (0.00 sec)

mysql> insert into department values(301,'人力');
Query OK, 1 row affected (0.00 sec)

mysql> insert into department values(302,'运营');
Query OK, 1 row affected (0.00 sec)

mysql> insert into employee(name,sex,age,dep_id) values ('陈裕光','male',18,200), ('乐珈彤','female',48,201), ('朱慧 珊','male',38,300), ('科琳·玛丽诺','female',28,301), ('伊万·伦德尔','male',18,302);
Query OK, 5 rows affected (0.01 sec)
Records: 5  Duplicates: 0  Warnings: 0
mysql> desc department;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(30) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)

mysql> desc employee;
+--------+-----------------------+------+-----+---------+----------------+
| Field  | Type                  | Null | Key | Default | Extra          |
+--------+-----------------------+------+-----+---------+----------------+
| id     | int(11)               | NO   | PRI | NULL    | auto_increment |
| name   | varchar(20)           | YES  |     | NULL    |                |
| sex    | enum('male','female') | NO   |     | male    |                |
| age    | int(11)               | YES  |     | NULL    |                |
| dep_id | int(11)               | YES  |     | NULL    |                |
+--------+-----------------------+------+-----+---------+----------------+
5 rows in set (0.01 sec)

mysql> select * from employee;
+----+-------------------+--------+------+--------+
| id | name              | sex    | age  | dep_id |
+----+-------------------+--------+------+--------+
|  1 | 陈裕光            | male   |   18 |    200 |
|  2 | 乐珈彤            | female |   48 |    201 |
|  3 | 朱慧珊            | male   |   38 |    300 |
|  4 | 科琳·玛丽诺       | female |   28 |    301 |
|  5 | 伊万·伦德尔       | male   |   18 |    302 |
+----+-------------------+--------+------+--------+
5 rows in set (0.00 sec)

mysql> select * from department;
+------+--------+
| id   | name   |
+------+--------+
|  200 | 技术   |
|  300 | 销售   |
|  301 | 人力   |
|  302 | 运营   |
+------+--------+
4 rows in set (0.00 sec)

不适用任何匹配条件。生成笛卡尔积
mysql> select * from employee,department;
+----+-------------------+--------+------+--------+------+--------+
| id | name              | sex    | age  | dep_id | id   | name   |
+----+-------------------+--------+------+--------+------+--------+
|  1 | 陈裕光            | male   |   18 |    200 |  200 | 技术   |
|  1 | 陈裕光            | male   |   18 |    200 |  300 | 销售   |
|  1 | 陈裕光            | male   |   18 |    200 |  301 | 人力   |
|  1 | 陈裕光            | male   |   18 |    200 |  302 | 运营   |
|  2 | 乐珈彤            | female |   48 |    201 |  200 | 技术   |
|  2 | 乐珈彤            | female |   48 |    201 |  300 | 销售   |
|  2 | 乐珈彤            | female |   48 |    201 |  301 | 人力   |
|  2 | 乐珈彤            | female |   48 |    201 |  302 | 运营   |
|  3 | 朱慧珊            | male   |   38 |    300 |  200 | 技术   |
|  3 | 朱慧珊            | male   |   38 |    300 |  300 | 销售   |
|  3 | 朱慧珊            | male   |   38 |    300 |  301 | 人力   |
|  3 | 朱慧珊            | male   |   38 |    300 |  302 | 运营   |
|  4 | 科琳·玛丽诺       | female |   28 |    301 |  200 | 技术   |
|  4 | 科琳·玛丽诺       | female |   28 |    301 |  300 | 销售   |
|  4 | 科琳·玛丽诺       | female |   28 |    301 |  301 | 人力   |
|  4 | 科琳·玛丽诺       | female |   28 |    301 |  302 | 运营   |
|  5 | 伊万·伦德尔       | male   |   18 |    302 |  200 | 技术   |
|  5 | 伊万·伦德尔       | male   |   18 |    302 |  300 | 销售   |
|  5 | 伊万·伦德尔       | male   |   18 |    302 |  301 | 人力   |
|  5 | 伊万·伦德尔       | male   |   18 |    302 |  302 | 运营   |
+----+-------------------+--------+------+--------+------+--------+
20 rows in set (0.00 sec)

```

#### 多表查询

```
SELECT 字段列表
    FROM 表1 INNER|LEFT|RIGHT JOIN 表2
    ON 表1.字段 = 表2.字段;
```
##### 内连接查询inner

找两张表共有的部分，相当于利用条件从笛卡尔积结果中筛选出了正确的结果

```

mysql> select employee.id,employee.name,employee.age,employee.sex,department.name,department.id from employee inner jooin department on employee.dep_id=department.id;
+----+-------------------+------+--------+--------+------+
| id | name              | age  | sex    | name   | id   |
+----+-------------------+------+--------+--------+------+
|  1 | 陈裕光            |   18 | male   | 技术   |  200 |
|  3 | 朱慧珊            |   38 | male   | 销售   |  300 |
|  4 | 科琳·玛丽诺       |   28 | female | 人力   |  301 |
|  5 | 伊万·伦德尔       |   18 | male   | 运营   |  302 |
+----+-------------------+------+--------+--------+------+
4 rows in set (0.01 sec)

mysql> select * from employee inner join department on employee.dep_id=department.id;
+----+-------------------+--------+------+--------+------+--------+
| id | name              | sex    | age  | dep_id | id   | name   |
+----+-------------------+--------+------+--------+------+--------+
|  1 | 陈裕光            | male   |   18 |    200 |  200 | 技术   |
|  3 | 朱慧珊            | male   |   38 |    300 |  300 | 销售   |
|  4 | 科琳·玛丽诺       | female |   28 |    301 |  301 | 人力   |
|  5 | 伊万·伦德尔       | male   |   18 |    302 |  302 | 运营   |
+----+-------------------+--------+------+--------+------+--------+
4 rows in set (0.00 sec)

```
##### 左连接
优先显示左表全部记录

- 以左表为准，即找出所有员工信息，当然包括没有部门的员工
- 本质就是：在内连接的基础上增加左边有右边没有的结果

```
mysql>  select employee.id,employee.name,department.name as depart_name from employee left join department on employee.dep_id=department.id;
+----+-------------------+-------------+
| id | name              | depart_name |
+----+-------------------+-------------+
|  1 | 陈裕光            | 技术        |
|  3 | 朱慧珊            | 销售        |
|  4 | 科琳·玛丽诺       | 人力        |
|  5 | 伊万·伦德尔       | 运营        |
|  2 | 乐珈彤            | NULL        |
+----+-------------------+-------------+
5 rows in set (0.00 sec)

```
##### 右连接

优先显示右表全部记录

- 以右表为准，即找出所有部门信息，包括没有员工的部门
- 本质就是：在内连接的基础上增加右边有左边没有的结果


```
mysql> select employee.id,employee.name,department.name as depart_name from employee right join department on employeee.dep_id=department.id;
+------+-------------------+-------------+
| id   | name              | depart_name |
+------+-------------------+-------------+
|    1 | 陈裕光            | 技术        |
|    3 | 朱慧珊            | 销售        |
|    4 | 科琳·玛丽诺       | 人力        |
|    5 | 伊万·伦德尔       | 运营        |
+------+-------------------+-------------+
4 rows in set (0.00 sec)
增加一条记录
mysql> insert into department values(12,'测试');
Query OK, 1 row affected (0.00 sec)

mysql> select employee.id,employee.name,department.name as depart_name from employee right join department on employee.dep_id=department.id;
+------+-------------------+-------------+
| id   | name              | depart_name |
+------+-------------------+-------------+
|    1 | 陈裕光            | 技术        |
|    3 | 朱慧珊            | 销售        |
|    4 | 科琳·玛丽诺       | 人力        |
|    5 | 伊万·伦德尔       | 运营        |
| NULL | NULL              | 测试        |
+------+-------------------+-------------+
5 rows in set (0.00 sec)

```
##### 全表连接

显示左右两个表的全部记录
- 全外连接：在内连接的基础上增加左边有右边没有的和右边有左边没有的结果
- 注意：mysql不支持全外连接 full JOIN
- 强调：mysql可以使用此种方式间接实现全外连接

```
mysql>  select * from employee left join department on employee.dep_id = department.id
    -> union
    ->  select * from employee right join department on employee.dep_id = department.id;
+------+-------------------+--------+------+--------+------+--------+
| id   | name              | sex    | age  | dep_id | id   | name   |
+------+-------------------+--------+------+--------+------+--------+
|    1 | 陈裕光            | male   |   18 |    200 |  200 | 技术   |
|    3 | 朱慧珊            | male   |   38 |    300 |  300 | 销售   |
|    4 | 科琳·玛丽诺       | female |   28 |    301 |  301 | 人力   |
|    5 | 伊万·伦德尔       | male   |   18 |    302 |  302 | 运营   |
|    2 | 乐珈彤            | female |   48 |    201 | NULL | NULL   |
| NULL | NULL              | NULL   | NULL |   NULL |   12 | 测试   |
+------+-------------------+--------+------+--------+------+--------+
6 rows in set (0.00 sec)

```
##### 符合条件连接查询

```
mysql>  select employee.name,department.name from employee inner join department on employee.dep_id=department.id where age>18;
+-------------------+--------+
| name              | name   |
+-------------------+--------+
| 朱慧珊            | 销售   |
| 科琳·玛丽诺       | 人力   |
+-------------------+--------+
2 rows in set (0.00 sec)

```
#### 子查询

- 子查询是将一个查询语句嵌套在另一个查询语句中。
- 内层查询语句的查询结果，可以为外层查询语句提供查询条件。
- 子查询中可以包含：IN、NOT IN、ANY、ALL、EXISTS 和 NOT EXISTS等关键字
- 还可以包含比较运算符：= 、 !=、> 、<等



