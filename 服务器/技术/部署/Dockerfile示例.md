#注意，docker命令全部大写，这是规定。
#   From 关键字表示，jar包依赖的环境。java:8  相当于jdk1.8
FROM java:8

#ADD命令 
#   docker-0.0.1-SNAPSHOT.jar：这是你上传jar包的名称。
#   /build_docke.jar：这是自定义的名称。但是注意要有之前的/
ADD server.jar /eureka_server.jar
ADD order.jar /eureka_order.jar


#MAINTAINER  作者名称。可以删除不写。
MAINTAINER zhouxf

#EXPOSE 项目暴露的端口号
EXPOSE 8761
EXPOSE 7900


#/build_docke.jar此处的名称要和ADD命令后面的一样。
ENTRYPOINT ["java","-jar","/eureka_server.jar"]
ENTRYPOINT ["java","-jar","/eureka_order.jar"]

HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -fs http://120.79.189.156:8761/ || exit 1
