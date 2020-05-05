
# 配置文件config
通过在.ssh/config中可以配置目的主机的别名、默认端口等。

config文件格式
Host 登录别名
    HostName 目的主机IP地址
    User 登录用户名
    Port 登录端口（默认是22）
    IdentityFile （密钥的绝对路径） --可选项 有更安全。免密码登陆
1
2
3
4
使用方法
ssh 登录别名
————————————————
版权声明：本文为CSDN博主「MichaelJay2015」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/u014132720/java/article/details/102763145

# 搬瓦工服务器没有密钥生产界面需要通过下面的方式生成密钥，上传到服务器指定目录后才可以。

ssh密钥登录(两种方法)

墨子哲 2012-02-28 16:35:17  82889  收藏 6
展开
方法一:

使用下例中ssky-keygen和ssh-copy-id，仅需通过3个步骤的简单设置而无需输入密码就能登录远程Linux主机。
ssh-keygen 创建公钥和密钥。
ssh-copy-id 把本地主机的公钥复制到远程主机的authorized_keys文件上。
ssh-copy-id 也会给远程主机的用户主目录（home）和~/.ssh, 和~/.ssh/authorized_keys设置合适的权限 。

步骤1: 用 ssh-key-gen 在本地主机上创建公钥和密钥
ligh@local-host$ ssh-keygen -t  rsa
Enter file in which to save the key (/home/jsmith/.ssh/id_rsa):[Enter key]
Enter passphrase (empty for no passphrase): [Press enter key]
Enter same passphrase again: [Pess enter key]
Your identification has been saved in /home/jsmith/.ssh/id_rsa.
Your public key has been saved in /home/jsmith/.ssh/id_rsa.pub.
The key fingerprint is: 33:b3:fe:af:95:95:18:11:31:d5:de:96:2f:f2:35:f9
ligh@local-host

步骤2: 用 ssh-copy-id 把公钥复制到远程主机上
ligh@local-host$ ssh-copy-id -i ~/.ssh/id_rsa.pub  root@192.168.0.3
ligh@remote-host‘s password:
Now try logging into the machine, with ―ssh ?remote-host‘‖, and check in:
.ssh/authorized_keys to make sure we haven‘t added extra keys that you weren‘t expecting.
[注: ssh-copy-id 把密钥追加到远程主机的 .ssh/authorized_key 上.]

步骤3: 直接登录远程主机
ligh@local-host$ ssh remote-host
Last login: Sun Nov 16 17:22:33 2008 from 192.168.1.2
[注: SSH 不会询问密码.]
ligh@remote-host$
[注: 你现在已经登录到了远程主机上]

https://blog.csdn.net/bravezhe/article/details/7302800

方法二

一、概述

1、就是为了让两个linux机器之间使用ssh不需要用户名和密码。采用了数字签名RSA或者DSA来完成这个操作

2、模型分析

假设 A （192.168.20.59）为客户机器，B（192.168.20.60）为目标机；

要达到的目的：
A机器ssh登录B机器无需输入密码；
加密方式选 rsa|dsa均可以，默认dsa

 

二、具体操作流程

 

单向登陆的操作过程（能满足上边的目的）：
1、登录A机器
2、ssh-keygen -t [rsa|dsa]，将会生成密钥文件和私钥文件 id_rsa,id_rsa.pub或id_dsa,id_dsa.pub
3、将 .pub 文件复制到B机器的 .ssh 目录， 并 cat id_rsa.pub >> ~/.ssh/authorized_keys
4、大功告成，从A机器登录B机器的目标账户，不再需要密码了；（直接运行 #ssh 192.168.20.60 ）