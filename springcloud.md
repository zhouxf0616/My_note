# redis命令
nohup ./redis-cli > /dev/null 2>&1 &
nohup java -jar xxx.jar >/dev/null 2>&1 &
# activemq 命令
nohup bin/activemq start  
或者：
我们也可以把日志输出到指定的日志文件中
nohup bin/activemq start > /tmp/smlog 2>&1 & 
查看状态
netstat -anlp | grep 8161