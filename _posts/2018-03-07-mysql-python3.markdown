---
layout:     post

title:      "Linux环境下Python3及Mysql安装配置"

subtitle:   ""

date:       2018-03-07 15:00

author:     "Wyq"

catalog:    true

tags:
   python
   mysql

---

# 前言

最近腾讯推出腾讯云服务器，10元/月，果断买了3年的，虽然配置不高，2G内存，
50G硬盘，1M带宽。跑个爬虫玩倒是足够了。下面是在服务器上安装mysql和python的历程。

# Linux环境下mysql数据库安装及配置
1. 首先下载安装源。`wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm`
2. 执行命令`rpm -ivh mysql-community-release-el6-5.noarch.rpm ` 。
3. yum安装`yum install mysql-community-server`。在此过程中会自动下载安装依赖，
遇到选择[y/N]的地方直接一路`y`就行了。

4. 至此，mysql安装完毕。然后是启动mysql：
`service mysqld start`
5. 一开始root密码为空，`mysql -uroot -p`然后回车进入mysql，接下来修改root密码。
* 选择库：`use mysql`
* 修改密码：`update user set password=password('test123') where user='root';`
注意不要写成`update user set password='test123' where User='root';`因为password函数会自动加密
* 退出mysql：`exit`
* 重新进入`mysql：mysql -uroot -p`，回车，输入自己的密码如`test123`，回车。

ok，搞定。现在使用mysql的连接工具如`navicat`就可以直接远程访问了。

# Linux下Python3安装

因Linux中默认情况下很多东西依赖于python2环境，比如yum。所以正常
情况下我们都选择直接安装python3，反正两者也不冲突。
1. 首先还是下载安装包。`wget https://www.python.org/ftp/python/3.6.0/Python-3.6.0a1.tar.xz`
2. 解压缩文件。`tar -xvf Python-3.6.0a1.tar.xz`
3.
    * 进入目录`cd Python-3.6.0a1`
    * 检查编译环境`./configure`

    *在此步骤我的环境报错`no acceptable C compiler found in $PATH`，
    安装gcc即可解决`yum -y install gcc`。*（安装完再次执行`./configure`，如果报错就根据错误情况去百度解决，
    直到不报错进入下一步）。
4. 开始安装`make && make install`。
5. 执行`python3`检查是否安装成功，成功后shell显示类似于下面；
```
Python 3.6.0a1 (default, Mar  7 2018, 16:16:52)
[GCC 4.8.5 20150623 (Red Hat 4.8.5-16)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

搞定，收工。

如果你遇到和我不同的问题，欢迎在本文下方留言（需要翻墙）。
或者[邮箱](393912540@qq.com)联系我。

[github源码地址  欢迎Fork ](https://github.com/ToBeNumber0/webpack-gulp-angular)   

本文原创，欢迎大家参考。