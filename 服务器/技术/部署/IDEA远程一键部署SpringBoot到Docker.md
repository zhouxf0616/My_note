# IDEA远程一键部署SpringBoot到Docker

https://www.liangzl.com/get-article-detail-145399.html

重新加载docker配置

systemctl daemon-reload // 1，加载docker守护线程
systemctl restart docker // 2，重启docker
3，查看firewall防火墙

(1)查看firewall服务状态

systemctl status firewalld
出现Active: active (running)切高亮显示则表示是启动状态。

出现 Active: inactive (dead)灰色表示停止，看单词也行。

(2)查询端口是否开放

firewall-cmd --query-port=2375/tcp
 

(3)如果没有开放就开放80端口

firewall-cmd --permanent --add-port=2375/tcp
(4)重启防火墙(修改配置后要重启防火墙)

firewall-cmd --reload