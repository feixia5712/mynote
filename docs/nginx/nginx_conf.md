### nginx配置文件

#### nginx配置文件

```
[root@localhost nginx]# pwd
/usr/local/nginx
[root@localhost nginx]# tree
.
├── client_body_temp
├── conf
│   ├── fastcgi.conf
│   ├── fastcgi.conf.default
│   ├── fastcgi_params
│   ├── fastcgi_params.default
│   ├── koi-utf
│   ├── koi-win
│   ├── mime.types
│   ├── mime.types.default
│   ├── nginx.conf
│   ├── nginx.conf.default
│   ├── scgi_params
│   ├── scgi_params.default
│   ├── uwsgi_params
│   ├── uwsgi_params.default
│   └── win-utf
├── fastcgi_temp
├── html
│   ├── 50x.html
│   └── index.html
├── logs
│   ├── access.log
│   ├── error.log
│   └── nginx.pid
├── proxy_temp
│   ├── 1
│   │   └── 00
│   ├── 2
│   │   └── 00
│   └── 3
│       └── 00
├── sbin
│   └── nginx
├── scgi_temp
└── uwsgi_temp

15 directories, 22 files

```

??? note "解释"
    ```
    Nginx的配置文件是一个纯文件文件，它位于nginx的安装目录的conf目录下，
    整个配置文件是以块的形式组织的，每个块一般是以一个“{}”来表示，块可以分为几个层次，
    整个配置文件中mian指令位于最高层，在mian层下面可以有Events，HTTP等层级，
    而在HTTP层中又包含有sever层，即是sever block，sever block中又可以分location层，
    并且一个sever block钟可以包含多个location block。

    ```

