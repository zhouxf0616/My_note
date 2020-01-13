# vue-cli（vue脚手架）超详细教程
https://blog.csdn.net/qq_40741855/article/details/87077521

npm 、cnpm 、node、vue  全都装上了，就是 webpack 装不上！！

最后我把整个服务器还原为初始设置了！( 自己的服务器，不怕，全部再重装就是了 )

但依旧不行！ 我想不出来怎么表达当时的心情 ...  薯片都没有心情吃了...

 

出现报错，报错大致如题。

解决方法：先全局安装少的这个：
npm install webpack-cli -g

再正常执行 webpack 安装命令：
npm install webpack -g
npm install webpack --save-dev