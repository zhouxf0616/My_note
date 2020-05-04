https://www.jianshu.com/p/169b3164336b

<zone>
  <short>Public</short>
  <description>For use in public areas. You do not trust the other computers on networks to not harm your computer. Only selected incoming connections are accepted.</description>
  <service name="dhcpv6-client"/>
  <service name="ssh"/>
  <port protocol="tcp" port="443"/>
  <port protocol="tcp" port="22"/>
  <port protocol="tcp" port="21"/>
  <port protocol="udp" port="53"/>
  <port protocol="tcp" port="8081"/>
  <port protocol="tcp" port="8080"/>
  <port protocol="tcp" port="80"/>
  <port protocol="tcp" port="9090"/>
  <port protocol="tcp" port="2222"/>
  <port protocol="tcp" port="3306"/>
</zone>

vim /etc/firewalld/zones/public.xml

systemctl start firewalld


firewall-cmd --reload








搬瓦工CentOS系统防火墙设置与端口开放方法
2019-06-04 分类：BandwagonHost 评论(2)
目录	
搬瓦工防火墙介绍
iptables防火墙设置
firewalld防火墙设置
端口开放检查方法
与Ubuntu/Debian系统不同，如果你的搬瓦工VPS使用的是CentOS系统，如果在启动了服务后，发现端口不通连不上，那么可能是因为还需要设置防火墙。CentOS 6默认内置的防火墙为iptables，CnetOS 7内置的防火墙为firewalld，本文介绍搬瓦工CentOS系统的防火墙设置与端口开放方法。

搬瓦工CentOS防火墙设置

 

搬瓦工防火墙介绍
搬瓦工VPS默认没有防火墙，但是如果你的系统是CentOS（查看系统类型：如何查看搬瓦工VPS的系统？如何更换搬瓦工系统版本？），那么如果你的搬瓦工VPS在运行了一些服务后，发现端口不通连不上，那么可能是需要设置防火墙，开放指定端口，例如在8080端口运行网络服务，以及修改SSH端口等。

CentOS 7之前内置的防火墙为iptables，升级到7后，内置的防火墙则变成了firewalld。接下来分别介绍搬瓦工CentOS 6和CentOS 7如何设置防火墙。

 

iptables防火墙设置
CentOS 6默认内置的防火墙为iptables。

1.打开/关闭/重启防火墙

开启防火墙(重启后永久生效)：chkconfig iptables on

关闭防火墙(重启后永久生效)：chkconfig iptables off

开启防火墙(即时生效，重启后失效)：service iptables start

关闭防火墙(即时生效，重启后失效)：service iptables stop

重启防火墙:service iptables restartd
2.查看防火墙打开的端口

/etc/init.d/iptables status
3.开放指定端口

此处以开放8088端口为例：

（1）开放端口

iptables -A INPUT -p tcp --dport 8088 -j ACCEPT
（2）保存并重启防火墙

/etc/rc.d/init.d/iptables save
/etc/init.d/iptables restart
4.开放指定范围的端口

例如开放1024-10240之间的所有端口：

iptables -A INPUT -p tcp --dport 1024:10240 -j ACCEPT
 

firewalld防火墙设置
CentOS 7默认内置的防火墙为firewalld。

[root@localhost ~]# systemctl start firewalld.service       --启动firewall
[root@localhost ~]# systemctl enable firewalld.service 

1.查看防火墙状态

systemctl status firewalld
此处如果提示firewalld.service could not be found.则说明你的系统没有装防火墙，则不需要设置。

2.开放指定端口

此处以开放8088端口为例：

firewall-cmd --zone=public --add-port=8088/tcp --permanent
–permanent参数表示永久生效，没有此参数重启后失效。

3.重启防火墙

firewall-cmd --reload #重启firewall
systemctl stop firewalld.service #停止firewall
systemctl disable firewalld.service #禁止firewall开机启动
firewall-cmd --state #查看默认防火墙状态（关闭后显示notrunning，开启后显示running）
 
