# 登陆
ssh -p 22 root@120.79.189.156

# redis命令
nohup ./redis-cli > /dev/null 2>&1 &
nohup java -jar xxx.jar >/dev/null 2>&1 &
netstat -lntp | grep 6379

>#使用客户端

>redis-cli shutdown

>#因为Redis可以妥善处理SIGTERM信号，所以直接kill-9也是可以的

>kill -9 PID

>如果执行上面导致Redis客户端连接不上或没有连接，可以重新启动Redis,打开这个文件目录下执行启动./etc/>init.d/redis-server如下：

>./etc/init.d/redis-server start

>./etc/init.d/redis-server stop

>./etc/init.d/redis-server restart

---
# activemq 命令

https://blog.csdn.net/qq_37469931/article/details/88921454

nohup bin/activemq start  
或者：
我们也可以把日志输出到指定的日志文件中
nohup bin/activemq start > /tmp/smlog 2>&1 & 
查看状态
netstat -anlp | grep 8161

> 1 启动 ： 进入到activeMQ 的 bin 目录，执行   ./activemq start  开启

> 2 查看activeMQ 是不是启动的状态， ./activemq  status

> 3 停止 activemq  命令 ./activemq  stop
---

# 通过cmd启动jar服务
找到jar的文件夹位置打开cmd

>1、java -jar xxxxx.jar  // 当前ssh窗口被锁定，可按CTRL + C打断程序运行，或直接关闭窗口，程序退出
>2、java -jar xxxxx.jar &   //当前ssh窗口不被锁定，但是当窗口关闭时，程序中止运行。
>3、nohup Java -jar xxxxxx.jar &  //意思是不挂断运行命令,当账户退出或终端关闭时,程序仍然运行



Linux 运行jar包命令(Cent OS 7后台运行jar包)
Linux 运行jar包命令如下：

 

方式一

java -jar shareniu.jar
特点：当前ssh窗口被锁定，可按CTRL + C打断程序运行，或直接关闭窗口，程序退出

那如何让窗口不锁定？

 

方式二

java -jar shareniu.jar &
&代表在后台运行。

特定：当前ssh窗口不被锁定，但是当窗口关闭时，程序中止运行。

继续改进，如何让窗口关闭时，程序仍然运行？

 

方式三

nohup java -jar shareniu.jar &
nohup 意思是不挂断运行命令,当账户退出或终端关闭时,程序仍然运行

当用 nohup 命令执行作业时，缺省情况下该作业的所有输出被重定向到nohup.out的文件中，除非另外指定了输出文件。

 

方式四

nohup java -jar shareniu.jar >/dev/null  &  
解释下 >temp.txt

command >out.file

command >out.file是将command的输出重定向到out.file文件，即输出内容不打印到屏幕上，而是输出到out.file文件中。

 

可通过jobs命令查看后台运行任务

jobs
那么就会列出所有后台执行的作业，并且每个作业前面都有个编号。
如果想将某个作业调回前台控制，只需要 fg + 编号即可。

fg 23
 

查看某端口占用的线程的pid

netstat -nlp |grep :9181



# nohup: 忽略输入并把输出追加到"nohup.out"

>执行nohup java -jar do_iptable.jar & 运行jar会提示：nohup: 忽略输入并把输出追加到"nohup.out"

>执行nohup java -jar do_iptable.jar >/dev/null  & 运行jar会提示：nohup: 忽略输入重定向错误到标准输出端

>修改运行方式为nohup java -jar do_iptable.jar >/dev/null 2>&1 &即可。

>>nohup java -jar chapter1-0.0.1-SNAPSHOT.jar >/dev/null 2>&1 &


服务器上启动可执行jar包，java -jar xxx.jar >log.out &，&表示关闭页面后后台继续执行