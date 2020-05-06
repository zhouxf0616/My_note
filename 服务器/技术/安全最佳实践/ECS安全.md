您好，针对服务器的系统安全，建议您定期做检查维护。
安全加固参考：
一.安全组建议您只放行需要对外访问的端口。
安全组规则可参考：https://help.aliyun.com/document_detail/25471.html
安全组应用案例参考：https://help.aliyun.com/document_detail/25475.html
安全组配置具体位置在：
控制台-云服务器ECS-点击相应实例后方的管理-本实例安全组-配置规则
二.快照方面
设置自动创建快照策略
自动创建快照策略：https://help.aliyun.com/document_detail/25456.html
定期手动创建快照：https://help.aliyun.com/document_detail/25455.html
三.服务器内部安全
建议定期做安全检查，对数据库，源码文件等重要文件在本地或其他云端也做好备份。
三.安全加固，将以下两个方向做好加固，最大程度上保证服务器安全。
操作系统加固：https://help.aliyun.com/knowledge_list/60787.html
web应用加固：https://help.aliyun.com/knowledge_list/60792.html




您好，如果您这边机器已经被黑客入侵，植入挖矿程序，建议您这边做好快照备份，重新初始化实例，重新部署环境，给出的理由如下：
1、您的机器已经被入侵，就算您能找到对应的挖矿程序，您也很难确认系统是否被做后门。
2、您的机器已经被入侵，不确定您的系统底层关键文件、模块、用户数据、程序数据是否被破坏；
3、系统的安全性无法得到保证

下面给出对应的教程
此问题建议您创建快照备份当前数据，再初始化系统盘恢复环境。 然后可拷贝快照里面的数据恢复。
1、确认相关磁盘的快照已经创建完成，创建快照的操作方法如下：
https://help.aliyun.com/document_detail/25455.html
2、在控制台打开购买云盘页面，购买【和服务器处于相同可用区】的云盘，选择从快照创建磁盘：https://help.aliyun.com/document_detail/32317.html
3、重新初始化系统盘
https://help.aliyun.com/document_detail/25449.html
4、恢复系统盘数据， 将第二步购买的快照盘在控制台上挂载到服务器上即可：
https://help.aliyun.com/document_detail/25446.html

您参考一下上方的教程，有问题您及时反馈。