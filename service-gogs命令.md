# 服务端启动某个服务
systemctl status/start/stop/restart [gogs]
service starter/force-restart/start [gogs]
# 后台启动gogs
./gogs web & 

# 查看指定端口进程
lsof -i:3000  
