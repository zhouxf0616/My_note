# tail -f 命令暂停方法
Linux 下查看日志时，使用

tail -f
可以不断的刷新日志信息。

例如:

tail -f logs.log
此时要想暂停刷新，使用ctrl+s暂停终端。
若想继续终端，使用ctrl+q。

若想退出tail命令，直接使用ctrl+c。