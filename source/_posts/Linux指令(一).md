---
title: linux命令(一)Ubuntu基础命令
date: 2020-03-01 20:43:52
categories:
- Tech 
- Command
- Linux
tags: [Linux, Command]
mathjax: false
urlname: linux_command_ubuntu
keywords: [hexo writting, tricks]
description:
---

{% note info %}

**说明**

本文是在大二下学期因疫情缘故无法返校时看韩顺平`linux`网课所做笔记，后并为勘误，如有错误，请谅解
{% endnote %}

<!--more-->

```shell 常用基础命令
# change directory，切换目录
cd

# 删除文件
rm -rf 文件名

# 查看网络配置
ifconfig

# 新建文件
touch 文件名

# 列出当前文件夹下面的目录
ls

# 写+退出
wq

# 查看文件内容
cat 文件名

# 使用vim编辑器编辑文件
vim 文件名		
```



# 实操篇

-------

## 1 vim 快捷键使用

#### 拷贝行 

+ yy 拷贝当前行	5yy 拷贝自上而下5行 

#### 粘贴行

+ p

#### 删除行 

+ dd 删除当前行	5dd 删除自上而下5行

#### 查找关键词 /关键字  

+ /关键字
+ 找到后再按n跳转到下一个关键字

#### 设置行号 

+ :set nu                     

#### 取消行号 

+ :set nonu

#### 光标到达最低行 

+ G(shift+g)  （本质是光标移动但之前没有输入数字，系统默认移动到最下面）                    

#### 到达首行 

+ gg       本质控制光标移动但之前没有输入数字，系统默认移动到最上面

#### 光标向下移动n行   

+ 数字n+回车或加下方向键

#### 撤销 

+ u

#### 重写

+ ctrl+r

#### 光标到达指定行

1. 设置行号 :set nu
2. 输入数字
3. 使用gg或者shift+g

##### 上述所有操作均在正常模式下进行

----

## 2 开机重启+用户登陆注销篇

### 开机重启

#### shutdown

+ shutdown -h now:表示立即关机
+ shutdown -h 1:表示1分钟后关机
+ shutdown -r now:立即重启

#### halt

+ halt:效果等价于关机

#### reboot

+ reboot:效果等价于重启

#### sync

+ sync:把内存的数据储存到磁盘
  + 重启时最好先执行sync指令

### 用户登录和注销（对于运行级别3下有效，如：Xshell时来说）

#### 意义

+ root 用户权限太高，可能会删除一些核心文件
+ 我们常用普通用户登录，登陆后再使用“su -用户名”命令来切换成管理员

#### 切换成管理员

+ su -用户名

#### 注销

+ logout

-------

## 3 用户管理

### 1 基本用户管理 

####  添加用户

+ useradd 用户名
  + 创建了一个用户和一个与用户同名的组，并将用户放进此组中
  + 将用户放进一个新创建的文件夹名与用户名相同的家目录中
+ useradd -d 目录 用户名
  + 创建一个用户和一个与用户同名的组，并将用户放进此组中
  + 将用户放进一个新创建的文件夹名为指定名字的家目录中

#### 指定或修改密码

+ passwd 用户名
  + 输入时密码不会显示，且要输入两次

#### 删除用户

+ userdel 用户名
  + 删除用户+保留家目录
+ userdel -r 用户名
  + 删除用户+删除家目录

#### 查询用户信息

+ id 用户名
  + 显示的是用户基本信息

#### 切换用户

+ su - 用户名
  + 注意空格（CentOS7后不需要加 - 了）
  + 从权限高用户切换到权限低用户时，需要密码，反之不用
  + 当需要返回原来用户时，使用exit

#### 查看当前用户

+ whoami
  + 显示名字

### 2 用户组管理

#### 增加组

+ groupadd 组名

#### 删除组

+ groupdel 组名

#### 增加用户到指定组

+ useradd -g 用户组名 用户名
  + 将新增用户指定到某个组

#### 修改用户组

+ usermod -g 用户组名 用户名
  + 将已存在用户更改到指定组

### 3 用户信息储存

#### 用户信息配置文件

+ 用户名:口令(用户密码):用户标识号:组标识号:注释性描述:主目录:登录 shell
+ 位置：/ect/passwd

#### 组信息配置文件

+ 组名:口令:组标识号:组内用户列表
+ 位置：/ect/group

#### 口令配置文件

+ 密码和登录信息，属于加密文件
+ 登录名:加密口令:最后一次修改时间:最小时间间隔:最大时间间隔:警告时间:不活动时间:失效时间:标志
+ 位置：/ect/shadow

## 4  实用指令

### 运行级别

![image-20200328165315188](https://cdn.jsdelivr.net/gh/Coldeye2020/picturebed/img/20200328165526.png)

#### 运行级别配置文件

+ 位置：/etc/inittab
+ 这个文件是可以用vim编辑的哟，所以也可以将其指定内容设置为不同级别（但是CentOS7及以上是使用其他方式了）

#### 切换到指定运行级别

+ init 数字（0-6之间的一个）
  + 每次切换运行级别后将需要重新登录（出了单用户模式）

#### 找回root密码

+ 每个系统和不同版本都不同（自行百度）https://blog.csdn.net/shanvlang/article/details/80385913

### 帮助指令

+ man 某个指令 
  + 获取该指令帮助信息
+ help 某个指令
  + 获得shell内置命令的帮助信息
+ 百度或谷歌

### 文件目录指令

之后复习再做整理

---------

## 5 组管理和权限管理

### 组管理

+ 意义

  + 对于每一个linux用户，至少要属于一个组，不能独立于组外
  + 对于每一个linux文件（包括目录），有所有者，所在组和其他组的概念
  + 一般来说文件的所有者就是创建者，所在组就是创建者的组。其他组代指其所有者用户，所在组的用户之外的所有用户

+ 文件操作（包括目录）

  + 查看文件的所有者以及所在组
    + ls -ahl
  + 修改文件的所有者
    + chown 用户名 文件名
  + 同时改变文件的所有者以及文件的所在组
    + chown 用户名:组名 文件名 
  + 改变目录以及其下所有文件的信息(递归)
    + chown -R 用户名:组名 文件名 

  + 修改文件的所在组
    + chgrp 组名 文件名

+ 用户操作

  + 查看用户信息
    + id 用户名
  + 修改用户所在组
    + usermod -g 组名
    + usermod -d 家目录名

### 权限管理

#### 权限详解

ls-l中显示的内容-rwxrw-r-- 1 root root 1213 Feb 2 09:39 abc

+ 0-9位说明

  1)第0位确定文件类型(d,-,l,c,b)

  2)第1-3位确定所有者（该文件的所有者）拥有该文件的权限。---User

  3)第4-6位确定所属组（同用户组的）拥有该文件的权限，---Group

  4)第7-9位确定其他用户拥有该文件的权限---Other

  + rwx作用到文件				

    1)[r]代表可读(read):可以读取,查看

    2)[w]代表可写(write):可以修改,但是不代表可以删除该文件,删除一个文件的前提条件是对该文件所在的目录有写权限，才能删除该文件.

    3)[x]代表可执行(execute):可以被执行

  + rwx作用到目录

    1)[r]代表可读(read):可以读取，ls查看目录内容

    2)[w]代表可写(write):可以修改,目录内创建+删除+重命名目录

    3)[x]代表可执行(execute):可以进入该目录

  + 可用数字表示为:r=4,w=2,x=1因此rwx=4+2+1=7

+ 第10位

  + 作用于目录时	代表目录下子目录数量（包括隐藏的）
  + 作用于文件时     硬链接数 

#### 修改文件权限-chmod

+ +、-、=变更权限

  + u:所有者 g:所有组 o:其他人 a:所有人(u、g、o的总和)

    1)chmod u=rwx,g=rx,o=x  文件目录名

    2)chmod   o+w       文件目录名

    3)chmod   a-x         文件目录名

+ 数字更变权限

  + r=4 w=2 x=1 , rwx=4+2+1=7，rx=5
  + chmod u=rwx,g=rx,o=x 文件目录名 相当于 chmod 751 文件目录名

-------------

## 6 任务调度

### 基本命令

+ 编辑任务调度
  + crontab -e
+ 查看当前任务调度
  + crontab -l
+ 终止（删除）当前任务调度
  + crontab -r
+ 重启任务调度
  + service crond restart

### 任务调度编辑基本语法

+ #### 时间部分 + 任务执行部分

+ #### 时间部分

  + 5个部分：分钟 小时 日期 月份 星期
  + <img src="C:\Users\大神哈哈\AppData\Roaming\Typora\typora-user-images\image-20200329142823572.png" alt="image-20200329142823572" style="zoom:50%;" />

<img src="C:\Users\大神哈哈\AppData\Roaming\Typora\typora-user-images\image-20200329142833796.png" alt="image-20200329142833796" style="zoom:50%;" />

+ #### 任务执行部分

  + 对于较简单的命令：可以直接在 crontab -e的编辑器下直接写

  + 对于较为复杂的命令：先写好一个包含完整操作指令的shell文件(.sh)，并将该文件的权限设置为可执行文件(744)

    再到crontab -e编辑器下直接运行

-----------------------

## 7 磁盘分区和挂载(mount)

### 1 查看系统中磁盘信息

+ 查看系统分区及挂载情况
  + lsblk -f（老师不离开）
+ 查看磁盘基本信息（包括大小）
  + lsblk 	

### 2 添加或移除磁盘(包含挂载)

+ #### 给虚拟机台添加/移除硬盘

  + 在VM软件中实现

+ #### 将硬盘空间分区

  + fdisk /dev/sdb
    + m显示命令列表	p显示磁盘分区同  fdisk –l	n新增分区	d删除分区	w写入并退出
  + 开始分区后输入n，新增分区，然后选择p(rimary)，分区类型为主分区。两次回车默认剩余全部空间。最后输入w写入分区并退出，若不保存退出输入q。

+ #### 格式化

  + mkfs -t ext4 /dev/sdb1
    + 其中ext4为分区类型

+ #### 临时挂载/卸载

  + mount   设备(位置和名称) 挂载目录
  + umount 设备(位置和名称)  or 挂载目录
    + 对于卸载任意选择其中一个系统就可以识别

+ #### 永久挂载/卸载

  + vim /etc/fstab 
  + 模仿其他行的书写格式写上
    + 设备(位置和名称) 或者 UUID       挂载目录      分区格式    defaults    0 0
  + mount   –a
    + 使挂载立即生效

### 3 查看系统磁盘使用整体情况

+ #### 查看整体情况

  + df -h

+ #### 查看指定目录占用情况情况 du

  + du -h 带计量单位

  + du -s 指定目录占用大小汇总

  + du -a 含文件

  + du --max-depth=1   子目录深度为1

  + du -c   列出明细的同时，增加汇总值

  + #### 常用        du -ach --max-depth=n 文件目录    

### 4 工作实用指令

+ #### 统计/home文件夹下文件的个数

  + ls -l /home | grep "^-" | wc -l

+ #### 统计/home文件夹下目录的个数

  + ls -l /home | grep "^d" | wc -l

+ #### 统计/home文件夹下所有文件的个数，包括子文件夹里的

  + ls -lR /home | grep "^-" | wc -l

+ #### 统计/home文件夹下所有文件的个数，包括子文件夹里的

  + ls -lR /home | grep "^d" | wc -l

+ #### 以树状结构查看目录

  + tree 文件目录
  + 如果没有就用 yum stall tree安装

## 8 网络配置

### 1 查询ip信息

+ #### windows

  + ipconfig

+ #### linux

  + ifconfig

### 2 查询是否联通

+ ping ipaddress 或者 网址域名

### 3 网络环境配置

+ #### 自动获取

  + 方式	
    + 可以直接在运行级别5环境下进行操作，即勾选DHCP
    + <img src="C:\Users\大神哈哈\AppData\Roaming\Typora\typora-user-images\image-20200329170700425.png" alt="image-20200329170700425" style="zoom:50%;" />
  + 缺点
    + 自动获取会导致ip地址是动态的，无法作为服务器

+ #### 手动设置

  + 方式
    + vim /etc/sysconfig/network-scripts/ifcfg-eth33
      + 注意，不同的版本文件可能名字不同，位置不同，需要具体查询
    + 具体需要注意几个点：IPADDR, GATEWAY, DNS1, BOOTPROTO, ONBOOT
    + ![image-20200329171204112](C:\Users\大神哈哈\AppData\Roaming\Typora\typora-user-images\image-20200329171204112.png)
    + service network restart
      + 重启网络服务

## 9 进程管理

### 1 进程查看

+ #### ps 

  + -a	显示当前终端的所有进程信息
  + -u    以用户的格式显示进程信息
  + -x	 显示后台进程运行的参数
  + -e     显示所有进程
  + -f      全格式

+ #### 查看所有进程信息

  + ps -aux 

+ #### 查看所有父进程

  + ps -ef | more

+ #### 查看某些进程信息

  + ps -aux | grep XXX(进程相关信息) | more

+ #### 查看进程树(更加直观)

  + pstree
    + -p     显示进程PID
    + -u     显示进程所属用户

  <img src="C:\Users\大神哈哈\AppData\Roaming\Typora\typora-user-images\image-20200329184234373.png" alt="image-20200329184234373" style="zoom:50%;" />

<img src="C:\Users\大神哈哈\AppData\Roaming\Typora\typora-user-images\image-20200329184553477.png" alt="image-20200329184553477" style="zoom:50%;" />

### 2 进程终止

+ #### kill 进程号(PID)

  + -9    表示强迫进程立即停止

+ #### killall 进程名称(一般是父进程)

  + 支持通配符
  + 删除进程下所有的子进程

### 3 服务查看

+ 服务的本质也是进程

+ #### 打开图形界面进行查看

  + setup

+ #### 查看所有服务及其状态

  + systemctl list-unit-files
  + /etc/init.d/服务名称    **(CentOS7之后就不行了)**
    + 常用 ls -l /ect/init.d

+ ####  查看单个服务的状态

  + systemctl status 服务名称（新）
  + service 服务名称 status（旧）

### 4 服务管理

+ #### 打开图形界面进行管理（永久生效:下次开机后不会还原）

  + setup

+ #### 终端操作（临时生效:下次开机后会还原）
  + service 服务名 [start|stop|restart|reload|status]
  + systemctl  [start|stop|restart|reload|status]  服务名

+ #### 终端操作（永久生效）

  + chkconfig 指令

+ #### 可以在win上进行检测端口是否被监听（不同服务对应不同端口）

  + telnet ipaddress 服务对应端口

### 5 在不同服务下的服务自启动

+ 由于每个系统的指令不一样
  + 这里就不展开了

### 6  动态监控进程（与ps的区别在于其实时更新）

+ top
  + ![image-20200329193752382](C:\Users\大神哈哈\AppData\Roaming\Typora\typora-user-images\image-20200329193752382.png)
  + 交互指令
    + u      输入用户名，并只显示属于该用户的进程
    + k      输入PID，并终止进程
    + P      以CPU使用率进行排序
    + M      以占用内存进行排序
    + N      以PID顺序进行排序
    + q       退出
  + 参数
    + -d 数字        每多少秒更新一次
    + -i                  使不显示僵死或限制进程
    + -p  PID          指定监控某个进程

## 10 RPM 与YUM

+ ### PRM（REDHAT Package Manager）

  + #### rpm包的查询

    + rpm -qa
      + 查询所有已经安装的rpm列表
    + rpm -qa | grep 软件包名
      + 查询单个包的安装信息
    + rpm -q 软件包名
      + 查询软件包是否安装
    + rpm -qi 软件包名
      + 查询软件包信息
    + rpm -ql 软件包名
      + 查询软件包中的文件
    + rpm -qf 文件全路径名
      + 查询文件所属的软件包（反过来查）

  + #### rpm包的卸载

    + rpm -e 软件包名
      + 删除rpm软件包
    + rpm -e -nodeps 软件包名
      + 强制删除

  + #### rpm包的安装

    + rpm -ivh RPM包全路径
      + i=install 安装
      + v=verbose 提示
      + h=hash  进度条

  + #### RPM包好像有点麻烦，不要细究了

+ ### YUM（Yellow dog Updater ,  Modified）

  + 查询yum服务器中是否有rpm包

    + yum -list | grep 软件包名

  + 安装rpm包

    + yum install 软件包名

  + 一些参数指令

    + -y 安装过程一律yes

  + 查看yum安装软件位置

    + ```
      cat /etc/yum.conf | grep cachedir
      ```

      



# JAVAEE 定制篇

## 1 环境搭建 

#### 	1 下载java

```shell
yum -y install java
```

#### 	2 检查java版本

```
java -version
```

+ 显示

```
openjdk version "1.8.0_242"
OpenJDK Runtime Environment (build 1.8.0_242-b08)
OpenJDK 64-Bit Server VM (build 25.242-b08, mixed mode)
```

#### 	3 手动配置全局变量（若没有显示，并提示java不是命令）

```shell
vi /etc/profile
```

+ 增加到末尾（目录根据实际的情况自行调整）

```
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.171-8.b10.el6_9.x86_64
export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$PATH:$JAVA_HOME/bin
```

#### 	4 全局变量立即生效

```
source /etc/profile
```

#### 	5 检查java是否生效

```
java -version
```

## 2 tomcat安装

# SHELL编程篇

```shell
#!/bin/bash
```

source

$()=``

unset

readonly

export

```
:<<!
ffagjkasj
!
```

$

后台运行程序

```
可执行文件 &
```

# Ubuntu

```shell
sudo apt-get update					 更新源
sudo apt-get install package		  安装包
sudo apt-get remove package			  删除包
sudo apt-cache search package          搜索软件包
sudo apt-cache show package            获取包的相关信息，如说明、大小、版本等
sudo apt-get install package--reinstall重新安装包
sudo apt-get-f install 				  修复安装
sudo apt-get remove package--purge	   删除包，包括配置文件等
sudo apt-get build-deppackage		  安装相关的编译环境
sudo apt-get upgrade                   更新已安装的包
sudo apt-get dist-upgrade              升级系统
sudo apt-cache depends package         了解使用该包依赖那些包
sudo apt-cache rdepends package        查看该包被哪些包依赖
sudo apt-get source package            下载该包的源代码
```

