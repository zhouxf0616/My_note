# 安装网桥工具
sudo yum install bridge-utils
# 查看docker0网桥
ip addr show docker0
# 显示所有网桥和关联容器  
brctl show
# docker0网桥下的容器 
brctl show docker0 

# 信息同步：
docker network ls

# 两个容器通过mybridge互连
docker network connect mybridge test1
docker network connect mybridge test2

# 查看mybridge信息 
docker network inspect mybridge：

# 查看指定容器的环境变量
docker exec test1 env

# 查看指定容器的host映射表
docker exec test1 cat /etc/hosts

当多个容器互联时，使用自定义bridge的方式，是最简单的。如果使用link, 需要通信的容器个数大于 2 个时复杂度会呈指数增长，或者，你可以编辑容器内的 /etc/hosts 文件，但这会产生难以调试的问题。自定义bridge是通过容器间自动 DNS 解析（automatic DNS resolution来实现容器互联的。

## 用户定义bridge和默认bridge docker0的区别
默认情况下，从容器发送到默认网桥的流量，并不会被转发到外部。要开启转发，需要改变两个设置。这些不是 Docker 命令，并且它们会影响 Docker 主机的内核。

配置 Linux 内核来允许 IP 转发
sysctl net.ipv4.conf.all.forwarding=1

改变 iptables 的政策，FORWARD 政策从 DROP 变为 ACCEPT
sudo iptables -P FORWARD ACCEPT
————————————————
版权声明：本文为CSDN博主「风格色」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_27068845/article/details/80893318