### 几种密钥配置

#### 1 普通用户切换到root免密

原理：

主要实现就是将普通用户生成的公钥放到root下，来实现免密登录

```
1登录时我们是普通用户进来
2 生成密钥
[zdk@localhost ~]$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/zdk/.ssh/id_rsa): 
Created directory '/home/zdk/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/zdk/.ssh/id_rsa.
Your public key has been saved in /home/zdk/.ssh/id_rsa.pub.
The key fingerprint is:
ab:4b:f9:bc:81:76:df:41:a9:cd:c6:f1:1c:33:67:dc zdk@localhost
The key's randomart image is:
+--[ RSA 2048]----+
|                 |
|                 |
|                 |
|             . ..|
|        S   + + E|
|       o . * + * |
|      = + . * o  |
|     o = o o .   |
|      o.+.. .    |
+-----------------+
[zdk@localhost ~]$ 
进入相关目录拷贝公钥
[zdk@localhost ~]$ cd .ssh/
[zdk@localhost .ssh]$ ls
id_rsa  id_rsa.pub
[zdk@localhost .ssh]$ ls -l id_rsa.pub 
-rw-r--r--. 1 zdk zdk 395 5月  24 06:31 id_rsa.pub
[zdk@localhost .ssh]$ cat id_rsa.pub 
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAzznqrMiaqBB4SkHh+XNmuT6wGg7aTTn7PBDOOxGAsEGDRWipiyekDsSFQjL1zNyEIJHUTQKov73vkWRE2irRwjXWTjecpVn3HMEyyInxbmNmS/hD4St9ij/FpLP562hZdi0sN4B8xd+VegVhPYStIlWIaZQ/XJi5Ao7o5y8xIs3rGBNwRoUOy9Q/yzIrFGp4E3NmqV9UcbMcJrmgZ3RPFbcLQI/H+hRElAg/4Vg3fANMxtOerhw/t1HiGg/z9/9kgW8CHjcttKjKBk6COifvwxtBzxD6W/FGCyAaaizIe175hgpkyvG1GBFPTGIAXU0gpmxFwD8T+Q8w19mmHGVHSQ== zdk@localhost
切换到root进入到相关目录
[root@localhost ~]# cd /root/.ssh/
[root@localhost .ssh]# ls
id_rsa  id_rsa.pub  known_hosts
创建authorized_keys，将刚才的公钥拷贝进去
[root@localhost .ssh]# touch authorized_keys
[root@localhost .ssh]# vim authorized_keys 
现在就可以实现普通用户案切换到root免密

[zdk@localhost ~]$ ssh root@::
The authenticity of host ':: (::)' can't be established.
RSA key fingerprint is 15:27:47:e9:c2:58:b5:e0:20:b0:c8:c3:a6:88:47:14.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '::' (RSA) to the list of known hosts.
Last login: Fri May 24 06:29:33 2019 from 192.168.94.1
```

#### 两台机器之间的免密登录

原理跟上面一样，主要将公钥拷贝到对方的authorized_keys 文件即可实现免密登录

