# 1. 以交互式创建并启动容器：

docker run -i -t –name dlgcy centos /bin/bash

 

# 2. 在容器命令行状态下键入 Ctrl+P Ctrl+Q 来回到宿主机；

 

# 3. 查看容器运行状态：

docker ps -a

 

# 4. 再次进入容器：

docker attach dlgcy

# 查看容器资源详情。
docker inspect 容器  