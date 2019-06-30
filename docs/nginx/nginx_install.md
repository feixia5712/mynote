### nginx安装

#### nginx简单介绍

Nginx本身是一款静态（html，css，js，jpg等）www软件 静态小文件高并发量，同时占用的资源很少，3W并发量 10个线程150w。

Nginx使用平台：unix linux,windows都可以

官网地址:http://nginx.org/

#### nginx的安装

1 安装pcre
  
PCRE 作用是让 Nginx 支持 Rewrite 功能。

```
yum install -y pcre-devel
或者
wget http://downloads.sourceforge.net/project/pcre/pcre/8.35/pcre-8.35.tar.gz
tar zxvf pcre-8.35.tar.gz
cd pcre-8.35
./configure && make && make install
查看是否已经安装
[root@localhost mynote]#  pcre-config  --version
7.8
```

2 nginx的安装

```
yum -y install pcre-devel openssl openssl-devel
useradd nginx -s /sbin/nologin -M
cd /usr/local/src
wget http://nginx.org/download/nginx-1.14.2.tar.gz
tar nginx-1.14.2.tar.gz
cd nginx-1.14.2
./configure --user=nginx --group=nginx --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module
make && make install
以上不报错代表安装成功 
```
3  启动并检查

```
检查配置文件:
[root@localhost sbin]# /usr/local/nginx/sbin/nginx -t
nginx: the configuration file /usr/local/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /usr/local/nginx/conf/nginx.conf test is successful
启动
[root@localhost sbin]# /usr/local/nginx/sbin/nginx
[root@localhost sbin]# ps -ef|grep nginx
root       1956      1  0 06:04 ?        00:00:00 nginx: master process /usr/local/nginx/sbin/nginx
nginx      1957   1956  0 06:04 ?        00:00:00 nginx: worker process      
root       1979   1874  0 06:04 pts/2    00:00:00 grep nginx
浏览器访问或者curl请求看是否启动成功
浏览器访问本机ip(端口默认是80)
curl请求
[root@localhost sbin]# curl 192.168.94.130:80 -I
HTTP/1.1 200 OK
Server: nginx/1.14.2
Date: Sat, 29 Jun 2019 22:06:52 GMT
Content-Type: text/html
Content-Length: 612
Last-Modified: Thu, 27 Jun 2019 22:04:53 GMT
Connection: keep-alive
ETag: "5d153d85-264"
Accept-Ranges: bytes

```


!!! note "*注意点*"
    检查nginx配置文件: /usr/local/nginx/sbin/nginx -t
    
    启动nginx:         /usr/local/nginx/sbin/nginx
    
    重新加载配置文件:  /usr/local/nginx/sbin/nginx -s reload

    nginx不通的排错
    
    1、ping ip  物理通不通
    
    2、telnet ip 浏览器到web服务器通不通
    
    3、服务器本地 curl  127.0.0.1 web服务开没开 
