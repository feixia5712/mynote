### mysql基本命令

#### 创建数据库
```
create database charset utf8
```
#### 创建表

```
create table info (id int,name varchar(15),sex enu('male','female'),age int(3))engine=innodb default charset=utf8
create table leco (id int(12) not null primary key auto_increment,name varchar(20),age int not null,score int not null)
```
#### 修改数据

```
update leco set id=4 where name='zdk'

```
#### 删除数据

```
delete from table_name [where 条件]
delete from leco where id=1
```
#### 清空表

```
truncate leco
delete from leco
```
#### 模糊查询

```
select * from where name like "z%"
select * from where name like "%z"
select * from where name like "%z%"
```
#### 去重distinct (只能用于select)

```
select distinct name from leco;
```
#### 限制语句返回次数

```
select * from leco limit 2
```
#### AND OR

```
select * from leco where name='alex' and age=90
select * from leco where name='alex' or age=80
```
#### 排序

```
select * from leco order by age desc 倒序
select * from leco order by age asc  正序
```
#### IN操作

```
select * from leco where age in(12,33)

```
#### 范围

```
select * from leco where age between 12 and 80
```
#### as别名

```
select name as "名字" from leco
```
#### 显示表的创建语句

```
show create table leco
```
#### 修改表的名字

```
alter table leco rename lecoo
```
#### 添加字段

```
alter table add addr varchar(10) first
alter table add addr varchar(20) after age
```
#### 删除字段

```
alter table leco drop addr
```
#### 修改字段

```
alter table leco modify hobby varchar(20)
alter table leco change hobby hobby1 varchar(39)
```
#### 给表添加主键

```
alter table leco add primary key(id)
```
#### 删除主键

```
alter table leco drop primary key
```
#### 增加复合组件

```
alter table leco add primary key(id,name)
```
#### 授权

```
grant 权限 on 数据库对象 to 用户 密码 其他
grant all privileges on *.* to 'zdk@123'@'%' identified by 'zdk@123' with grant option

```




??? note "解释说明"
    ```
    1. all privileges：表示将所有权限授予给用户。也可指定具体的权限，如：SELECT、CREATE、DROP等。

    2. on：表示这些权限对哪些数据库和表生效，格式：数据库名.表名，这里写“*”表示所有数据库，所有表。如果我要指定将权限应用到test库的user表中，可以这么写：test.user

    3. to：将权限授予哪个用户。格式：”用户名”@”登录IP或域名”。%表示没有限制，在任何主机都可以登录。比如：'zdk'@'192.168.0.%'，表示caimengzhi这个用户只能在192.168.0 该IP段登录

    4. identified by：指定用户的登录密码

    5. with grant option：表示允许用户将自己的权限授权给其它用户，一般用不到，最好有BDA统一管理。

    6. 可以使用GRANT给用户添加权限，权限会自动叠加，不会覆盖之前授予的权限，比如你先给用户添加一个SELECT权限，后来又给用户添加了一个INSERT权限，那么该用户就同时拥有了SELECT和INSERT权限。
    ```
#### 查看授予哪些权限
```
 show grants for 'cmz'@'%';
```
#### 授予某库的所有表

```
grant all privileges on db.* to 'cmz'@'%' identified by 'cmz';
```
#### 授予某库某表

```
grant all privileges on db.table1 to 'cmz'@'%' identified by 'cmz';

```
#### 授予某一个权限

```
grant create on db1.* to 'cmz'@'%';
```
