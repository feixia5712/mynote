### ss-local 终端代理（gfwlist）

#### 简介

ss-local 是 shadowsocks 的本地 socks5 服务器，如果需要使用 ss-local 提供的 socks5 代理，必须让应用程序使用 socks5 协议与之通信。但是很可惜，除了部分浏览器、软件直接支持 socks5 协议外，其它的都只支持 http 代理。因此，我们需要借助 privoxy 来将 http 代理协议转换为 socks5 代理协议，与后端的 ss-local 进行通信，与此同时我们还可以进行 gfwlist 分流操作。

#### 安装

为简单起见，这里选择安装 python 版 shadowsocks，当然你可以选择自己喜欢的任意版本（ss、ssr、ssh、v2ray，只要能提供 socks5 代理）。

```
# CentOS/RHEL
yum -y install epel-release
yum -y install python-pip
pip install shadowsocks

# ArchLinux
pacman -S python-pip
pip install shadowsocks

```
#### 配置


vim /etc/ss-local.json
{
    "server": "1.2.3.4",
    "server_port": 8989,
    "method": "aes-128-cfb",
    "password": "123456",
    "local_address": "127.0.0.1",
    "local_port": 1080,
    "fast_open": true,
    "workers": 1
}

## 配置说明

```

vim /etc/ss-local.json
{
    "server": "1.2.3.4",
    "server_port": 8989,
    "method": "aes-128-cfb",
    "password": "123456",
    "local_address": "127.0.0.1",
    "local_port": 1080,
    "fast_open": true,
    "workers": 1
}

## 配置说明：{
    "server": "1.2.3.4",          # 服务器IP
    "server_port": 8989,          # 服务器Port
    "method": "aes-128-cfb",      # 加密方式
    "password": "123456",         # 端口密码
    "local_address": "127.0.0.1", # 本地监听IP
    "local_port": 1080,           # 本地监听Port
    "fast_open": true,            # TCP Fast Open
    "workers": 1                  # worker进程数量}
```
#### 运行

```
nohup sslocal -c /etc/ss-local.json </dev/null &>>/var/log/ss-local.log &

```
