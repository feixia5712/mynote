#### 概要

vmware服务器支持snmp协议,借助其trap,发送告警日志到服务器,(比如服务器重启,或者其他操作),这里我们配置如何在服务器端接收配置好的告警(snmp协议发送过来的)

#### 配置

```
1 yum安装snmp
yum install net-snmp
yum install -y net-snmp-utils

2 修改配置文件

cat > /etc/snmp/snmptrapd.conf <<EOF

doNotFork no
disableAuthorization yes
ignoreAuthFailure yes
authCommunity log,execute,net public
traphandle .1.3.6.1.4.6876.* /data/scripts/snmptrap.sh vmware
traphandle .1.2.6.1.4.1.2.* /data/scripts/snmptrap.sh ibm
traphandle default /data/scripts/snmptrap.sh IBM-DW-SAMPLE::nodeDown
traphandle default /data/scripts/snmptrap.sh default
EOF
3 脚本内容如下
脚本主要是获取并且解析得到的日志,记录到文件中
cat > /data/scripts/snmptrap.sh << EOF

#/usr/bin/env bash
read host
read ip
vars=
while read oid val
do
   if [ ${vars} = "" ];then
      vars="${oid}${val}"
   else
       vars="{vars},${oid}${val}"
   fi
done
time=${`date "+%F %T"`}
echo "${time}${ip}${vars}" >>/data/snmp/${1}.log
EOF

4 启动

snmptraped -C -c /etc/snmp/snmptrapd.conf -A -Ln -Oqts -n -p /var/run/snmptrapd.pid -m +ALL

5 在vmware(vcenter)上配置告警选择snmp协议填写上地址 x.x.x.x:162  udp协议

6 触发告警时看在服务端是否接收到日志
```

