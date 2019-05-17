### Chrony服务

#### 简介

Chrony是一个开源的自由软件，像CentOS 7或基于RHEL 7操作系统，已经是默认服务，默认配置文件在 /etc/chrony.conf 它能保持系统时间与时间服务器（NTP）同步，让时间始终保持同步。相对于NTP时间同步软件，占据很大优势。其用法也很简单。
Chrony有两个核心组件，分别是：chronyd：是守护进程，主要用于调整内核中运行的系统时间和时间服务器同步。它确定计算机增减时间的比率，并对此进行调整补偿。chronyc：提供一个用户界面，用于监控性能并进行多样化的配置。它可以在chronyd实例控制的计算机上工作，也可以在一台不同的远程计算机上工作。

#### 配置说明

```
$ cat /etc/chrony.conf

# 使用pool.ntp.org项目中的公共服务器。以server开，理论上你想添加多少时间服务器都可以。
# Please consider joining the pool (http://www.pool.ntp.org/join.html).
server 0.centos.pool.ntp.org iburst
server 1.centos.pool.ntp.org iburst
server 2.centos.pool.ntp.org iburst
server 3.centos.pool.ntp.org iburst

# 根据实际时间计算出服务器增减时间的比率，然后记录到一个文件中，在系统重启后为系统做出最佳时间补偿调整。
driftfile /var/lib/chrony/drift

# chronyd根据需求减慢或加速时间调整，
# 在某些情况下系统时钟可能漂移过快，导致时间调整用时过长。
# 该指令强制chronyd调整时期，大于某个阀值时步进调整系统时钟。
# 只有在因chronyd启动时间超过指定的限制时（可使用负值来禁用限制）没有更多时钟更新时才生效。
makestep 1.0 3

# 将启用一个内核模式，在该模式中，系统时间每11分钟会拷贝到实时时钟（RTC）。
rtcsync

# Enable hardware timestamping on all interfaces that support it.
# 通过使用hwtimestamp指令启用硬件时间戳
#hwtimestamp eth0
#hwtimestamp eth1
#hwtimestamp *

# Increase the minimum number of selectable sources required to adjust
# the system clock.
#minsources 2

# 指定一台主机、子网，或者网络以允许或拒绝NTP连接到扮演时钟服务器的机器
#allow 192.168.0.0/16
#deny 192.168/16

# Serve time even if not synchronized to a time source.
local stratum 10

# 指定包含NTP验证密钥的文件。
#keyfile /etc/chrony.keys

# 指定日志文件的目录。
logdir /var/log/chrony

# Select which information is logged.
#log measurements statistics tracking
```

#### 常用一些命令

```
查看当前系统时区
timedatectl

查看所有可用时区
timedatectl list-timezones

设置当前系统时区

timedatectl set-timezone Asia/Shanghai

设置完时区后，强制同步下系统时钟：

chronyc -a makestep

手动同步
chronyc sources

查看同步状态

chronyc sources -v

校准时间服务器：
chronyc tracking

加入开机启动

$ systemctl enable chronyd.service
$ systemctl restart chronyd.service
$ systemctl status chronyd.service
```

#### 服务端配置

服务端配置只需要简单修改下server的地址即可

#### 客户端配置

客户端配置很简单，只需要将server的地址改为服务端的ip即可

