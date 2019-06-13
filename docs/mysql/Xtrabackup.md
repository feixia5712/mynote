### Xtrabackup

#### 介绍

Xtrabackup是一个对InnoDB做数据备份的工具，支持在线热备份（备份时候不影响数据读写），是商业备份工作InnoDB hotbackup的一个很好的替代品。

#### 特点

Xtrabackup是由percona提供的mysql数据库备份工具，据官方介绍，这也是世界上惟一一款开源的能够对innodb和xtradb数据库进行热备的工具。特点：
(1)备份过程快速、可靠；
(2)备份过程不会打断正在执行的事务；
(3)能够基于压缩等功能节约磁盘空间和流量；
(4)自动实现备份检验；
(5)还原速度快；

[下载网址](http://www.percona.com/software/percona-xtrabackup/)

#### centos上安装

1 安装Percona XtraBackup Percona yum资源库
```
yum install -y http://www.percona.com/downloads/percona-release/redhat/0.1-3/percona-release-0.1-3.noarch.rpm
yum list
如果下载速度慢的话,可以换成国内的清华源
sed -i "s/http:\/\/repo.percona.com\/release/https:\/\/mirror.tuna.tsinghua.edu.cn\/percona\/release/g" `grep -rl "repo.percona.com" /etc/yum.repos.d/percona-release.repo`

```
2 安装版本的选择
```
查看Percona XtraBackup版本
yum list|grep percona
percona-xtrabackup-20.x86_64                2.0.8-587.rhel6              percona-release-x86_64
percona-xtrabackup-20-debuginfo.x86_64      2.0.8-587.rhel6              percona-release-x86_64
percona-xtrabackup-20-test.x86_64           2.0.8-587.rhel6              percona-release-x86_64
percona-xtrabackup-21.x86_64                2.1.9-746.rhel6              percona-release-x86_64
percona-xtrabackup-21-debuginfo.x86_64      2.1.9-746.rhel6              percona-release-x86_64
percona-xtrabackup-22.x86_64                2.2.13-1.el6                 percona-release-x86_64
percona-xtrabackup-22-debuginfo.x86_64      2.2.13-1.el6                 percona-release-x86_64
percona-xtrabackup-24-debuginfo.x86_64      2.4.14-1.el6                 percona-release-x86_64

如果你的mysql版本>=5.7,那么你需要安装24及以上,以下安装22版本
我这里是mysql5.7的版本,所以需要安装24版本

```


??? note "注意点"
    ```
    假如你一不小心安装错了,在你使用的时候会有如下提示,版本不对
    [root@localhost ~]# innobackupex --user=root --password=123456 /opt/

    InnoDB Backup Utility v1.5.1-xtrabackup; Copyright 2003, 2009 Innobase Oy
    and Percona LLC and/or its affiliates 2009-2013.  All Rights Reserved.

    This software is published under
    the GNU GENERAL PUBLIC LICENSE Version 2, June 1991.

    Get the latest version of Percona XtraBackup, documentation, and help resources:
    http://www.percona.com/xb/p

    190614 05:48:20  innobackupex: Executing a version check against the server...
    190614 05:48:20  innobackupex: Connecting to MySQL server with DSN 'dbi:mysql:;mysql_read_default_group=xtrabackup' as 'root'  (using password: YES).
    190614 05:48:20  innobackupex: Connected to MySQL server
    190614 05:48:20  innobackupex: Done.
    190614 05:48:20  innobackupex: Connecting to MySQL server with DSN 'dbi:mysql:;mysql_read_default_group=xtrabackup' as 'root'  (using password: YES).
    190614 05:48:20  innobackupex: Connected to MySQL server
    innobackupex: got a fatal error with the following stacktrace: at /usr/bin/innobackupex line 4799
	main::check_server_version() called at /usr/bin/innobackupex line 1572
    innobackupex: Error: Unsupported server version: '5.7.24-log' Please report a bug at https://bugs.launchpad.net/percona-xtrabackup
    ```
3 开始安装

```
[root@localhost ~]# yum install -y percona-xtrabackup-24
已加载插件：fastestmirror
设置安装进程
Loading mirror speeds from cached hostfile
 * base: mirror.jdcloud.com
 * extras: ap.stykers.moe
 * updates: ap.stykers.moe
解决依赖关系
--> 执行事务检查
---> Package percona-xtrabackup-24.x86_64 0:2.4.14-1.el6 will be 安装
--> 处理依赖关系 libev.so.4()(64bit)，它被软件包 percona-xtrabackup-24-2.4.14-1.el6.x86_64 需要
--> 完成依赖关系计算
错误：Package: percona-xtrabackup-24-2.4.14-1.el6.x86_64 (percona-release-x86_64)
          Requires: libev.so.4()(64bit)
 You could try using --skip-broken to work around the problem
 You could try running: rpm -Va --nofiles --nodigest
```


??? note "错误解决" 
    ```
    yum install epel-release
    安装 epel源即可
    ```
4 继续安装

```
[root@localhost ~]# yum install percona-xtrabackup-24
已加载插件：fastestmirror
设置安装进程
Loading mirror speeds from cached hostfile
 * base: mirror.jdcloud.com
 * epel: mirrors.njupt.edu.cn
 * extras: ap.stykers.moe
 * updates: ap.stykers.moe
解决依赖关系
--> 执行事务检查
---> Package percona-xtrabackup-24.x86_64 0:2.4.14-1.el6 will be 安装
--> 处理依赖关系 libev.so.4()(64bit)，它被软件包 percona-xtrabackup-24-2.4.14-1.el6.x86_64 需要
--> 执行事务检查
---> Package libev.x86_64 0:4.03-3.el6 will be 安装
--> 完成依赖关系计算

依赖关系解决

=====================================================================================================================
 软件包                           架构              版本                     仓库                               大小
=====================================================================================================================
正在安装:
 percona-xtrabackup-24            x86_64            2.4.14-1.el6             percona-release-x86_64            8.2 M
为依赖而安装:
 libev                            x86_64            4.03-3.el6               epel                              113 k

事务概要
=====================================================================================================================
Install       2 Package(s)

总文件大小：8.3 M
Installed size: 8.3 M
确定吗？[y/N]：y
下载软件包：
warning: rpmts_HdrFromFdno: Header V4 RSA/SHA256 Signature, key ID 8507efa5: NOKEY
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-Percona


仓库 "Percona-Release YUM repository - x86_64" 的 GPG 密钥已安装，但是不适用于此软件包。请检查仓库的公钥 URL 是否配置正确。
```

??? note "解决办法"
    ```
    跟新源
    yum update percona-release
    ```
5 继续安装

```
yum install -y percona-xtrabackup-24
rpm -qa|grep xtrabackup
percona-xtrabackup-22-2.2.13-1.el7.x86_64
安装成功
```
6 简单使用测试(终于成功)

```
报错
[root@localhost ~]# innobackupex --defaults-file=/etc/my.cnf --user=root -password='123456' --database=root -socket=/tmp/mysql.sock /opt/

InnoDB Backup Utility v1.5.1-xtrabackup; Copyright 2003, 2009 Innobase Oy
and Percona LLC and/or its affiliates 2009-2013.  All Rights Reserved.

This software is published under
the GNU GENERAL PUBLIC LICENSE Version 2, June 1991.

Get the latest version of Percona XtraBackup, documentation, and help resources:
http://www.percona.com/xb/p

190614 05:31:15  innobackupex: Executing a version check against the server...
190614 05:31:15  innobackupex: Connecting to MySQL server with DSN 'dbi:mysql:;mysql_read_default_file=/etc/my.cnf;mysql_read_default_group=xtrabackup;mysql_socket=/tmp/mysql.sock' as 'root'  (using password: YES).
innobackupex: got a fatal error with the following stacktrace: at /usr/bin/innobackupex line 3006
	main::mysql_connect('abort_on_error', 1) called at /usr/bin/innobackupex line 1551
innobackupex: Error: Failed to connect to MySQL server as DBD::mysql module is not installed at /usr/bin/innobackupex line 3006.
190614 05:31:15  innobackupex: Connecting to MySQL server with DSN 'dbi:mysql:;mysql_read_default_file=/etc/my.cnf;mysql_read_default_group=xtrabackup;mysql_socket=/tmp/mysql.sock' as 'root'  (using password: YES).
innobackupex: got a fatal error with the following stacktrace: at /usr/bin/innobackupex line 3006
	main::mysql_connect('abort_on_error', 1) called at /usr/bin/innobackupex line 1570
innobackupex: Error: Failed to connect to MySQL server as DBD::mysql module is not installed at /usr/bin/innobackupex line 3006.
[root@localhost ~]# innobackupex -host=127.0.0.1 --defaults-file=/etc/my.cnf --user=root -password='123456' --database=root  /opt/
[root@localhost ~]# innobackupex -host=127.0.0.1 --defaults-file=/etc/my.cnf --user=root -password='123456' --database=root  /opt/

InnoDB Backup Utility v1.5.1-xtrabackup; Copyright 2003, 2009 Innobase Oy
and Percona LLC and/or its affiliates 2009-2013.  All Rights Reserved.

This software is published under
the GNU GENERAL PUBLIC LICENSE Version 2, June 1991.

Get the latest version of Percona XtraBackup, documentation, and help resources:
http://www.percona.com/xb/p

190614 05:33:45  innobackupex: Executing a version check against the server...
190614 05:33:45  innobackupex: Connecting to MySQL server with DSN 'dbi:mysql:;mysql_read_default_file=/etc/my.cnf;mysql_read_default_group=xtrabackup;host=127.0.0.1' as 'root'  (using password: YES).
innobackupex: got a fatal error with the following stacktrace: at /usr/bin/innobackupex line 3006
	main::mysql_connect('abort_on_error', 1) called at /usr/bin/innobackupex line 1551
innobackupex: Error: Failed to connect to MySQL server as DBD::mysql module is not installed at /usr/bin/innobackupex line 3006.
190614 05:33:45  innobackupex: Connecting to MySQL server with DSN 'dbi:mysql:;mysql_read_default_file=/etc/my.cnf;mysql_read_default_group=xtrabackup;host=127.0.0.1' as 'root'  (using password: YES).
innobackupex: got a fatal error with the following stacktrace: at /usr/bin/innobackupex line 3006
	main::mysql_connect('abort_on_error', 1) called at /usr/bin/innobackupex line 1570
innobackupex: Error: Failed to connect to MySQL server as DBD::mysql module is not installed at /usr/bin/innobackupex line 3006.

```

??? note "解决办法"
    ```
    查看mysql.so依赖的lib库
    ldd /usr/lib64/perl5/auto/DBD/mysql/mysql.so
    linux-vdso.so.1 =>  (0x00007fff7af8b000)
    libmysqlclient.so.16 => not found
    libz.so.1 => /lib64/libz.so.1 (0x00007f52741c3000)
    libcrypt.so.1 => /lib64/libcrypt.so.1 (0x00007f5273f83000)
    libnsl.so.1 => /lib64/libnsl.so.1 (0x00007f5273d63000)
    libm.so.6 => /lib64/libm.so.6 (0x00007f5273adb000)
    libssl.so.10 => /usr/lib64/libssl.so.10 (0x00007f527386b000)
    libcrypto.so.10 => /usr/lib64/libcrypto.so.10 (0x00007f527347b000)
    libc.so.6 => /lib64/libc.so.6 (0x00007f52730e3000)
    libfreebl3.so => /lib64/libfreebl3.so (0x00007f5272edb000)
    libgssapi_krb5.so.2 => /lib64/libgssapi_krb5.so.2 (0x00007f5272c93000)
    libkrb5.so.3 => /lib64/libkrb5.so.3 (0x00007f52729a3000)
    libcom_err.so.2 => /lib64/libcom_err.so.2 (0x00007f527279b000)
    libk5crypto.so.3 => /lib64/libk5crypto.so.3 (0x00007f527256b000)
    libdl.so.2 => /lib64/libdl.so.2 (0x00007f5272363000)
    /lib64/ld-linux-x86-64.so.2 (0x0000558df48cf000)
    libkrb5support.so.0 => /lib64/libkrb5support.so.0 (0x00007f5272153000)
    libkeyutils.so.1 => /lib64/libkeyutils.so.1 (0x00007f5271f4b000)
    libresolv.so.2 => /lib64/libresolv.so.2 (0x00007f5271d2b000)
    libpthread.so.0 => /lib64/libpthread.so.0 (0x00007f5271b03000)
    libselinux.so.1 => /lib64/libselinux.so.1 (0x00007f52718db000)
    发现libmysqlclient.so.16缺少
    查看mysql-x86_64.conf
    [root@mysql ~]# cat /etc/ld.so.conf.d/mysql-x86_64.conf
    /usr/lib/mysql
    /usr/local/mysql/lib  #这里我把mysql安装在/usr/local/mysql路径下
    find / -name libmysqlclient.so.16
    >:/usr/lib64/mysql/libmysqlclient.so.16
    cp /usr/lib64/mysql/libmysqlclient.so.16.0.0 /lib64/libmysqlclient.so.16
    最后在查看
    [root@localhost mysql]# !ldd
    ldd /usr/lib64/perl5/auto/DBD/mysql/mysql.so
	linux-vdso.so.1 =>  (0x00007ffd6f78b000)
	libmysqlclient.so.16 => /lib64/libmysqlclient.so.16 (0x00007fe7cdd53000)
	libz.so.1 => /lib64/libz.so.1 (0x00007fe7cdb33000)
	libcrypt.so.1 => /lib64/libcrypt.so.1 (0x00007fe7cd8f3000)
	libnsl.so.1 => /lib64/libnsl.so.1 (0x00007fe7cd6d3000)
    这样就可以了
    ```
7 最后验证终于成功
```
innobackupex --defaults-file=/etc/my.cnf --user=root -password='123456' --database=root /opt/
```

