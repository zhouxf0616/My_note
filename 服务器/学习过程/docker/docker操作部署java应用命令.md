## 在服务器中创建一个文件夹DockerTest用于存放上传的springboot jar包，我创建的文件夹名

进入步骤1中创建的文件夹，使用vim命令创建并编辑文件，文件名称为：Dockerfile。用于存放编写打包镜像的配置。

注意：文件名称必须为这个名字，不然之后要指定文件名。强烈建议不要改名字。

命令如下：
```
vim Dockerfile
```
## 进入编辑界面。将一下的配置按照自己实际的进行修改。修改后保存退出。回到命令窗口界面。

```
#注意，docker命令全部大写，这是规定。
#   From 关键字表示，jar包依赖的环境。java:8  相当于jdk1.8
FROM java:8
 
#ADD命令 
#   docker-0.0.1-SNAPSHOT.jar：这是你上传jar包的名称。
#   /build_docke.jar：这是自定义的名称。但是注意要有之前的/
ADD docker-0.0.1-SNAPSHOT.jar /build_docke.jar
 
#MAINTAINER  作者名称。可以删除不写。
MAINTAINER zhangxiaosan
 
#EXPOSE 项目暴露的端口号
EXPOSE 8080
 
#/build_docke.jar此处的名称要和ADD命令后面的一样。
ENTRYPOINT ["java","-jar","/build_docke.jar"]
```

## 然后运行如下指令构建

```
docker build -t build_docke:v1 .
 
说明:
  build_docke   代表要打包成的镜像名称。按照自己实际情况写。
  :v1   代表版本号，可以不写则默认为latest
  .    代表为当前目录。这就是为什么一直在步骤一文件夹中进行操作,并且Dockerfile在此文件夹中的原因。
 
若之前Dockerfile不在步骤一的文件夹中 则需要指定到对应的地址。【不建议】
```

## 运行镜像，命令如下：
```
docker run --name build_docke -d -p 8080:8080 build_docke:v1
```
说明：
    build_docke：运行时给镜像取的别名，自定义。
    -d 代表要后台运行。
    -p 代表要在后面要映射端口。
    8080:8080 前者为docker的原项目端口，后者为服务器的端口且服务器要开放此端口。
    build_docke  镜像的名称。
    :v1   镜像的标签或者是版本号。为latest时可以不指定

结果如下：
## 查看docker images 正在运行的镜像状态 
```
docker ps -a
```
## 查看docker images
```
docker images
```
## 可以使用命令：docker logs 运行的镜像id   来查看运行日志
```
docker logs 运行的镜像id
```

> 如果出现这个错误
Error response from daemon: driver failed programming external connectivity on endpoint image_server (9587fe498f5860ac83b659d3c5ab98810345a677605a8ee4b9e5efba2bdcd5dc): Bind for 0.0.0.0:8761 failed: port is already allocated
```
重启docker服务后再启动容器
systemctl restart docker
docker start foo
```
 

# 列出本机正在运行的容器
```
docker container ls
```

# 列出本机所有容器，包括终止运行的容器
``` 
docker container ls --all

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                        PORTS               NAMES
649a6b785a86        ubuntu              "bash"              10 minutes ago      Exited (137) 9 minutes ago                        loving_austin
85b9c705e73f        hello-world         "/hello"            10 minutes ago      Exited (0) 10 minutes ago                         silly_lumiere
c9281ad7f7b8        ubuntu              "bash"              17 minutes ago      Exited (127) 11 minutes ago                       stupefied_curran
e06bf36259ef        hello-world         "/hello"            24 minutes ago      Exited (0) 24 minutes ago                         flamboyant_chaplygin
ig:~ itguang$
```

## 可以看出,我现在已经有了四个容器,终止运行的容器文件依然会占用硬盘空间,可以使用docker container rm [container_id]命令删除.
```
docker container ls --all

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                        PORTS               NAMES
c9281ad7f7b8        ubuntu              "bash"              22 minutes ago      Exited (127) 17 minutes ago                       stupefied_curran
e06bf36259ef        hello-world         "/hello"            29 minutes ago      Exited (0) 29 minutes ago                         flamboyant_chaplygin
ig:~ itguang$ docker container rm c9281ad7f7b8 e06bf36259ef
```



常用命令
镜像相关
docker search java：在Docker Hub（或阿里镜像）仓库中搜索关键字（如java）的镜像
docker pull java:8：从仓库中下载镜像，若要指定版本，则要在冒号后指定
docker images：列出已经下载的镜像
docker rmi java：删除本地镜像
docker build：构建镜像
容器相关
docker run -d -p 91:80 nginx ：在后台运行nginx，若没有镜像则先下载，并将容器的80端口映射为宿主机的91端口。
-d：后台运行
-P：随机端口映射
-p：指定端口映射
-net：网络模式
docker ps：列出运行中的容器
docker ps -a ：列出所有的容器
docker stop 容器id：停止容器
docker kill 容器id：强制停止容器
docker start 容器id：启动已停止的容器
docker inspect 容器id：查看容器的所有信息
docker container logs 容器id：查看容器日志
docker top 容器id：查看容器里的进程
docker exec -it 容器id /bin/bash：进入容器
exit：退出容器
docker rm 容器id：删除已停止的容器
docker rm -f 容器id：删除正在运行的容器
所有命令
docker
docker COMMAND --help
构建镜像
确定镜像模板：如java、nginx
新建Dockerfile文件
使用Dockerfile的指令完善Dockerfile的内容
在Dockerfile文件的所在路径执行docker build -t imageName:tag .，-t指定镜像名称，末尾的点标识Dockerfile文件的路径
执行docker run -d -p 92:80 imageName:tag即可

作者：张东冬
链接：https://www.jianshu.com/p/ca1623ac7723
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。