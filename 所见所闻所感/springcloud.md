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

# nohup: 忽略输入并把输出追加到"nohup.out"

>执行nohup java -jar do_iptable.jar & 运行jar会提示：nohup: 忽略输入并把输出追加到"nohup.out"

>执行nohup java -jar do_iptable.jar >/dev/null  & 运行jar会提示：nohup: 忽略输入重定向错误到标准输出端

>修改运行方式为nohup java -jar do_iptable.jar >/dev/null 2>&1 &即可。

>>nohup java -jar chapter1-0.0.1-SNAPSHOT.jar >/dev/null 2>&1 &


服务器上启动可执行jar包，java -jar xxx.jar >log.out &，&表示关闭页面后后台继续执行