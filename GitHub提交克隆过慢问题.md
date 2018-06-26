#GitHub Clone慢 Push慢 Pull慢

##问题:几十kb/s的clone速度

>###1. 在hosts文件添加 两个地址
>```
>151.101.113.194 github.global.ssl.fastly.net
192.30.253.113 github.com
>```
>终端 输入
>```
>vi /etc/hosts
>```
>进入 hosts 文件, 在最末尾 添加上面两个地址 然后Esc  ＋ :wq 保存退出
>
>###2.1 第一个地址怎么确定?
>点击这个链接 [查询](http://github.global.ssl.fastly.net.ipaddress.com)
>
>输入要查询的域名 : github.global.ssl.fastly.net
>
>####2.2 第二个地址怎么确定?
>点击这个链接 [查询](http://tool.chinaz.com/dns/)
>
>输入要查询的域名 : github.com
>
>具体参考这个帖子 [github访问慢和clone慢解决方案](https://blog.csdn.net/ITleaks/article/details/80351680) 你就知道 ``` 192.30.253.113 ``` 这个ip是怎么确定的
>
>
>

##参考链接
[1.github访问慢和clone慢解决方案](https://blog.csdn.net/sinat_38843093/article/details/79716804)

[2.GitHub clone 速度过慢的问题](https://blog.csdn.net/ITleaks/article/details/80351680)



