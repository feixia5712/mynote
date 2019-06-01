### mysql的安装

#### 1安装包的区别

glibc 与普通的 rpm包，glibc是编译后的版本,在安装的时候无需编译,rpm包是linux发行版带的包

#### MySQL5.7.17数据库glibc版本安装方法

1 下载地址

国内几个开源的地址
??? note "国内几个开源的地址"
    ```
    [搜狐mysql](http://mirrors.sohu.com/mysql/)
    [other](http://mirrors.ustc.edu.cn/mysql-ftp/Downloads/)
    ```
2 开始安装

```
下载mysql

tar zxf mysql-5.7.17-linux-glibc2.5-x86_64.tar.gz
mv mysql-5.7.17-linux-glibc2.5-x86_64 /usr/local/mysql 

groupadd -r mysql
useradd -r -g mysql mysql -c "MySQL Server" -d /dev/null -s /sbin/nologin
yum -y install numactl
mkdir -p /data/mysql
chown -R mysql:mysql /data/mysql  #一定要有这一步，不然初始化之后启动会失败，因为你初始化写的是mysql用户
/usr/local/mysql/bin/mysqld --initialize --basedir=/usr/local/mysql --datadir=/data/mysql --user=mysql --explicit_defaults_for_timestamp     #会生成一个临时密码需要记录下来
mkdri -p /var/lib/mysql
chown mysql:mysql /var/lib/mysql
启动
/usr/local/mysql/bin/mysqld_safe  --datadir=/data/mysql  &

```

??? note "注意点"
    ```
    注意查看mysql_safe启动的mysql的socket路径
    [root@localhost ~]# ps -ef|grep mysql
    root       1835   1372  0 06:02 pts/0    00:00:00 /bin/sh /usr/local/mysql/bin/mysqld_safe --datadir=/data/mysql
    mysql      1989   1835  0 06:02 pts/0    00:00:00 /usr/local/mysql/bin/mysqld --basedir=/usr/local/mysql --datadir=/data/mysql --plugin-dir=/usr/local/mysql/lib/plugin --user=mysql --log-error=/var/log/mysqld.log --pid-file=/var/run/mysqld/mysqld.pid --socket=/var/lib/mysql/mysql.sock
    ```
3继续安装

```
/usr/local/mysql/bin/mysql_secure_installation 默认的socket是/tmp/socket 

[root@localhost ~]# /usr/local/mysql/bin/mysql_secure_installation 
Securing the MySQL server deployment.

Enter password for user root:
Error: Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)

这样的话在启动的时候指定soxket
/usr/local/mysql/bin/mysql_secure_installation --socket=/var/lib/mysql/mysql.sock
root@215706:/usr/local/mysql# /usr/local/mysql/bin/mysql_secure_installation

Securing the MySQL server deployment.

Enter password for user root:

The existing password for the user account root has expired. Please set a new password.

New password:

Re-enter new password:

VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No:
Using existing password for root.
Change the password for root ? ((Press y|Y for Yes, any other key for No) : no

 ... skipping.
By default, a MySQL installation has an anonymous user,
allowing anyone to log into MySQL without having to have
a user account created for them. This is intended only for
testing, and to make the installation go a bit smoother.
You should remove them before moving into a production
environment.

Remove anonymous users? (Press y|Y for Yes, any other key for No) : y
Success.


Normally, root should only be allowed to connect from
'localhost'. This ensures that someone cannot guess at
the root password from the network.

Disallow root login remotely? (Press y|Y for Yes, any other key for No) : n   

 ... skipping.
By default, MySQL comes with a database named 'test' that
anyone can access. This is also intended only for testing,
and should be removed before moving into a production
environment.


Remove test database and access to it? (Press y|Y for Yes, any other key for No) : y
 - Dropping test database...
Success.

 - Removing privileges on test database...
Success.

Reloading the privilege tables will ensure that all changes
made so far will take effect immediately.

Reload privilege tables now? (Press y|Y for Yes, any other key for No) : y
Success.

```
接下来进行配置

```
ln -s /usr/local/mysql/bin/mysql /usr/bin/mysql
ln -s /usr/local/mysql/bin/mysqladmin /usr/bin/mysqladmin
ln -s /usr/local/mysql/bin/mysqldump /usr/bin/mysqldump
ln -s /usr/local/mysql/bin/mysql_config /usr/bin/mysql_config
ln -s /usr/local/mysql/lib/libmysqlclient.so.20.3.4 /usr/lib/libmysqlclient.so.20.3.4
```
创建mysql的配置文件

```

cat >/etc/ld.so.conf.d/mysql-x86_64.conf<<'eof'
/usr/lib/mysql
/usr/local/mysql/lib
eof
ldconfig

cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql
service mysql status

mkdir -p /etc/mysql/conf.d/
cat >/etc/my.cnf<<'eof'
[client]
port            = 3306
socket          = /tmp/mysql.sock

[mysqld_safe]
pid-file        = /data/mysql/mysqld.pid
socket          = /tmp/mysql.sock
nice            = 0

[mysqld]
init_connect='SET NAMES utf8mb4'
character-set-server = utf8
skip-host-cache
skip-name-resolve
user            = mysql
pid-file        = /data/mysql/mysqld.pid
socket          = /tmp/mysql.sock
port            = 3306
basedir         = /usr/local/mysql
datadir         = /data/mysql
tmpdir          = /tmp
log_error       = /data/mysql/error.log
lc-messages-dir = /usr/local/mysql/share
log_bin_trust_function_creators=1
explicit_defaults_for_timestamp
max_connections = 1000
log-output=FILE
general-log=1
general_log_file= /data/mysql/query.log   #记录mysql操作的所有数据
symbolic-links=0
!includedir /etc/mysql/conf.d/

[mysql]
default-character-set = utf8mb4
eof

cat >/etc/mysql/conf.d/performance-tuning-16GB.cnf<<'eof'
[mysqld]
skip-external-locking
max_allowed_packet = 1M
net_buffer_length = 8K
read_rnd_buffer_size = 512K
key_buffer_size = 512M
table_open_cache = 2048
sort_buffer_size = 8M
read_buffer_size = 8M
myisam_sort_buffer_size = 128M
thread_cache_size = 256
query_cache_size = 256M
tmp_table_size = 256M

explicit_defaults_for_timestamp = true
max_connections = 1000
max_connect_errors = 100
open_files_limit = 65535

#log-bin=mysql-bin    #看需求,可加也可以不加
binlog_format=mixed
server-id   = 1
expire_logs_days = 10
early-plugin-load = ""


default_storage_engine = InnoDB
innodb_data_home_dir = /data/mysql
innodb_data_file_path = ibdata1:10M:autoextend
innodb_log_group_home_dir = /data/mysql
innodb_buffer_pool_size = 2048M
innodb_log_file_size = 512M
innodb_log_buffer_size = 8M
innodb_flush_log_at_trx_commit = 1
innodb_lock_wait_timeout = 50
innodb_file_format = Barracuda
innodb_file_per_table = 1
eof
```

开启mysql
一般在这之前先杀死，刚才启动的然后在启动

```
/etc/init.d/mysql start
或者
systemctl enable mysql.service 即可
```
启动成功之后,mysql安装完毕

