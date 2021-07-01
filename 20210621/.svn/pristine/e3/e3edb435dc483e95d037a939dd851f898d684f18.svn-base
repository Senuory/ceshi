# Linux

## 1.Linux的前世今生

C语言-----unix----linux(内核开源)---发行版----作为服务器的操作系统使用



unix:HP-UNIX,AIX,Solaris

stallman:自由软件之父,GNU

linus:linux之父.他开放了Linux的内核.Git

linux的常见发行版:centos

服务器市场:90%+  Unix/Linux

google:基于linux推出了Android



作为测试的你,上班后,将要对公司的服务器进行各种测试环境的安装,因为只有安装上环境才能测试你要测的系统

一句话说穿:**测试学linux的目的,是为了的部署测试环境**

学习路线:基本命令----各种环境搭建(3种安装方式)----docker





## 2.安装

1.vm虚拟机

2.centos6.9

3.远程链接工具:putty,CRT,Xshell,SSH

​    ip:192.168.1.89	用户名:root		密码:111111



## 3.基础

### 1.目录结构(背)

/:根目录,所有目录的父目录,类似与'我的电脑'



用户:

/root:超管目录

/home:所有用户的目录



软件:

/usr:软件的默认安装目录

**/etc:配置文件目录(重要)**

/var:软件的工作目录或变化目录



设备:

/dev:device设备目录

/mnt:mount挂载外接设备



临时:

/tmp:temp,临时文件目录,工作后做试验一般在这个目录做



### 2.前缀

[root@localhost ~]#   整个这一串我们称为shell,linux自带的是bash shell

unix是csh

windows是winshell

root:当前用户

​	切换用户:su

​		超管----普通:su caichang

​		普通----超管:su -  需要root的密码

localhost:机器名

~:当前用户的工作目录

​	超管:/root

​	普通:/home/用户名

#:超管权限

$:普通权限



### 4.基本命令(超级重点)

#### 1.最基本命令

```shell
#pwd:查看当前所在位置
#举场景:我上班后,我的同事有环境搭建不起来,找我帮忙.我来到他的座位,坐下来就敲?
#不会,我会看看你到底现在在哪!如果你在的目录就是我要的目录,于是就敲,如果不是我要的目录,就切换目录
[root@localhost tmp]# pwd
/tmp/a/b/c/tmp

#cd:切换目录
#cd ..   退一层
#cd ../../../ 退三层
#相对路径,绝对路径 (带/就绝对)
#相对路径,相当于windows的双击文件夹
[root@localhost tmp]# pwd
/tmp
我想进入的是/tmp/a,即我已经在tmp下,想进入tmp下的目录,直接敲目录名即可
[root@localhost tmp]# cd a  

绝对路径
[root@localhost tmp]# pwd
/tmp
我想进入/var/www/html
[root@localhost tmp]# cd /var/www/html

#ls:当前目录下的内容
我们常常喜欢用ll,因为他是ls -l的缩写

一个问题产生,ls中-l是什么? 答:参数
又产生一个问题,我怎么看一个命令都有哪些参数? 答:man 命令
回车:往下看,q:退出


#alias:别名
命名:
alias cai='ls -l'

取消:
unalias cai
```



#### 2.文件系统

linux是一个文件系统,把所有的东西都看成文件,因此我们要学习文件和文件夹的操作

操作:新建,删除,重命名,复制,粘贴,剪切,查找

文件:查看文件内容

```shell
#新建
#文件夹:mkdir
mkdir caichang
mkdir caichang baobao fengjie
mkdir -p caichang/baobao/fengjie

#文件 touch
touch caichang.txt
touch baobao.txt fengjie.java fanbb.c

#删除
rmdir 文件夹   #他几乎不用,忘记都可以  他只能删除空文件夹
rm -rf 文件夹/文件   #删除时看清楚名,否则只能哭
	-r:递归   -f:强制
	
#重命名和剪切都是一个命令
#如果是同层,就表示重命名,否则表示剪切
mv 源目录 现目录


#复制
#如果是文件夹,带-r参数
cp 源目录 现目录

#查找
find 目录 -name '*文件*'

#查看文件内容
#先执行这个命令,拿到一个文件:cp /etc/httpd/conf/httpd.conf /tmp

#静态(很重要):
cat 文件名 #只适合看几行,十几行的小文件
more 文件名 #回车:一行一行的看  空格:一页一页的看,不能往上看
less 文件名 #上下看

#工作中,很多时候都是用more来看.而且很多时候你会听到这样的话:摸一下你就知道
#骚操作(暂时不管):
head -n 10 文件名
tac 文件名

#动态:(一般用在看日志上)(必会)
tail -f 文件名
```



#### 3.vi(必会)

vi是linux上的编辑器,简单理解成linux自带的记事本

1.模式切换

![](Linux/image-20210622152713813.png)

注意:

1.命令---编辑:a,i,o

​	a:append 追加,在光标后插入数据

​	i:insert 插入,在光标前插入数据

​	o:other,在光标下一行插入数据

2.末行模式技巧

​	1.w,q,!   w:write  q:quit   !:强制

​		:wq       :w       :q!         :q

​	 2.set number   set nonumber



**2.命令技巧**

我们vi的很多技巧都集中在命令模式中

1.移动光标

​	**上下:nG**

​	左右:w.e

​	上下左右:hjkl    **小键盘的上下左右**

​	右:空格 	左:删除键(backspace)

[补充]:每一行的行首都有一个^,行尾都有一个$.只是隐藏着

2.复制----粘贴

复制:y

​	一行:yy	n行:nyy   	光标到行首:y^		光标到行尾:y$

粘贴:p

3.删除:d

一行:dd	n行:ndd   	光标到行首:d^		光标到行尾:d$

4.微调:x

5.撤销:u

6.查找:/	n:向下		N:向上



3.扩展

请下来后自己百度并找出你觉得'爽'的技巧





#### 4.压缩/解压缩方案

Linux提供的方案:打包,压缩

打包:tar

```shell
#压缩
tar cvf 包名.tar 文件/文件夹

#解压
tar xvf 包名.tar

#查看包内容
tar -tf 包名.tar

#追加内容到包内
tar -rf 包名.tar 文件/文件夹

#删除包中内容
tar --delete -f 包名.tar 文件/文件夹
```



压缩:gzip

```shell
#压缩
gzip 包名.tar

#解压缩,但打包还在
gunzip 包名.tar.gz
```



**注意:上班喜欢一次性压缩和一次性解压缩**

```shell
#一次性压缩
tar zcvf 包名.tar.gz 文件/文件夹

#一次性解压缩
tar zxvf 包名.tar.gz
```



#### 5.用户管理

用户管理针对工作不是很重,但权限一定要会

1.用户管理

```shell
#新建用户
useradd libb
#赋予libb密码
passwd libb   ---->赋2次

#删除
userdel libb
#删除后,home下还会有文件夹,手动删除即可

#新建用户组
#当我们新建一个用户后,就会自动的新建一个同名的用户组
groupadd ui

#删除用户组
groupdel ui

#修改文件的所属用户
chown 用户名 文件/文件夹

#修改文件的所属用户组
chgrp 用户组名 文件/文件夹

#补充
#查看用户文件
more /etc/passwd

#查看用户组文件
more /etc/group
```



**2.权限(必会)**

```shell
drwxr-xr-x. 3 root     root      4096 Jun 21 02:12 zhiwenbo

rwxr-xr-x
```

1. 读

   rwx	rwx	rwx

   r:读  		4

   w:写		 2

   x:执行	  1

   读法:几几几  最高:777	最低:000

   rwxr-xr-x   :755

2. 理解

   rwx		rwx		rwx

   宿主	   宿组	   其他

   u			 g		    o

  3.认知权限

先看是否是宿主,如果是,就看前三

​                            如果不是,就看是否是宿组,如果是,就看中三

​                                                                        如果不是,就看后三

总之:要么前三,要么中三,要么后三



-rwxrw-r-- 		fengjie		testing		Hello.java

testing:caichang meizi xiaoqiang

dev:fengjie fanbb cai10

ui:wuyi rongrong chenming



**4.学会赋权(必会)**

```shell
#chmod

#1.最常见
chmod 777 文件
chmod -R 777 文件夹

#2.较常见
chmod +x 文件

#3.较常见
chmod u+x 文件

#4.不多见
chmod g+u 文件

```

#### 6.系统管理

```shell
#查看CPU
more /proc/cpuinfo

#查看内存
more /proc/meminfo

#查看硬盘
df -h
#查看具体的目录下的所有目录占用情况
#要先进入这个目录,否则这个*没有意义 *表示所有
du -sh *

#查看ip
#注意,centos7不用这套,用的是:ip addr
ifconfig

#启动某服务
#centos7启服务不这样,用:systemctl 状态 服务名       systemctl start firewalld.service
service 服务名(查,问) 状态(start,stop,restart)
```

#### 7.进程管理(必会)

```shell
#查看进程
#查看时关注第二列:pid(进程号)
ps -ef 或 ps aux
#查看指定的进程
#|:管道  grep:过滤字符串  abc:你要查的进程名 如图叫没有该进程
[root@localhost ~]# ps -ef | grep abc
root      3354  3335  0 23:37 pts/0    00:00:00 grep abc

#如下叫有该进程   service httpd start
[root@localhost ~]# ps -ef | grep httpd
root      3382     1  0 23:39 ?        00:00:00 /usr/sbin/httpd
apache    3385  3382  0 23:39 ?        00:00:00 /usr/sbin/httpd
apache    3386  3382  0 23:39 ?        00:00:00 /usr/sbin/httpd
apache    3387  3382  0 23:39 ?        00:00:00 /usr/sbin/httpd
apache    3388  3382  0 23:39 ?        00:00:00 /usr/sbin/httpd
apache    3389  3382  0 23:39 ?        00:00:00 /usr/sbin/httpd
apache    3390  3382  0 23:39 ?        00:00:00 /usr/sbin/httpd
apache    3391  3382  0 23:39 ?        00:00:00 /usr/sbin/httpd
apache    3392  3382  0 23:39 ?        00:00:00 /usr/sbin/httpd
root      3399  3335  0 23:40 pts/0    00:00:00 grep httpd


#杀死进程
#-9 强制
kill -9 pid 

killall/pkill 进程名


```



## 4.部署环境

上班后,开发给了我们做好的项目的代码,各种文档等,我们需要把这些代码能够'跑'起来,那么我们就需要安装各种环境来支撑这个项目

### 1.Linux中的三种安装方式

#### 1.rpm安装

rpm（英文全拼：redhat package manager） 原本是 Red Hat Linux 发行版专门用来管理 Linux 各项套件的程序，由于它遵循 成 规则且功能强大方便，因而广受欢迎。逐渐受到其他发行版的采用。RPM 套件管理方式的出现，让 Linux 易于安装，升级，间接提升了 Linux 的适用度。

```shell
#查看是否安装过
rpm -qa #很多
rpm -qa | grep 要查询的包名

#安装(最重要)
rpm -ivh 包名.rpm

#安装到哪
rpm -ql 包

#卸载
rpm -e 查出来的包名(rpm -qa | grep 要查询的包名)
```

rpm的包依赖:安装mysql



rpm优势和不足:

优势:安装方便

不好:不能配置安装路径等;离线安装方式;有严重的包依赖问题(很痛苦)



#### 2.yum安装

Yum（全称为 Yellow dog Updater, Modified）是一个在Fedora和RedHat以及CentOS中的Shell前端软件包管理器。基于RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软件包，无须繁琐地一次次下载、安装

```shell
#安装
yum install -y php

#切换源
#我们用的是华中科技大学,原因是:centos6.9只有他维护着,工作后一般用7的话,采用的是阿里云
http://mirrors.hust.edu.cn/help.html#centos

#清除并重生成
yum clean all
yum makecache
```

yum的优势和不足:

优势:在线安装,自动安装包和包依赖

不足:有网络,默认源慢,得切换国内源,我想装某版本的软件没办法的,只能用源内置的(除非切源),不能自定义安装路径等.



#### 3.源码安装

Linux上几乎所有的软件都经过了GPL授权，因此几乎所有的软件都会提供源码。 而一个软件要在Linux上执行，必须是二进制文件，因此当我们拿到软件源码后，需要将它编译成二进制文件才能在Linux上运行。

步骤:

1.获取源码(xxxx.tar.gz)

2.解压并进入目录

3.创建Makefile文件

4.编译

5.安装



案例:部署nginx服务器

```shell
cd /usr/local/
mkdir nginx
wget https://nginx.org/download/nginx-1.9.9.tar.gz
tar zxvf nginx-1.9.9.tar.gz
cd nginx-1.9.9
./configure --prefix=/usr/local/nginx/ --with-http_ssl_module
make
make install

make会出错,出错后执行,执行完成后,删除Makefile文件后重新./configure
yum -y install gcc gcc-c++ autoconf automake
yum -y install zlib zlib-devel openssl openssl-devel pcre pcre-devel

#测试
进入nginx的相关目录启动脚本,访问http://linux的ip即可
```



源码的优势和不足:

优势:可以自定义安装位置等诸多信息

不足:编译器不足,需要升级



### 2.jdk+tomcat+mysql+项目

1.安装jdk

通过rpm方式已安装

2.安装tomcat

```shell
#1.上传tomcat的文件到/tmp
#2.解压并复制一份到/usr/java并重命名成tomcat8080
#3.进入/usr/java/tomcat8080/bin,启动tomcat(startup.sh)
#4.测试:打开浏览器,输入:htpp://linux的ip:8080,如看到tomcat主界面即安装成功
```

3.安装mysql

通过rpm安装了mysql.但是很遗憾,你windows通过navicat没有办法访问linux中的mysql,原因是要开启mysql的远程访问权限

```shell
#1.进入mysql
mysql
#2.切换到mysql数据库
use mysql;
#3.通过更新user表的host字段:从localhost--->%,%表示所有人都能访问
update user set host='%' where user='root' and host='localhost';
#4.刷新
FLUSH PRIVILEGES;
#5.退出mysql
exit;
#6.重启mysql服务器
service mysqld restart
#7.测试:重新打开navicat,输入对应的服务器信息,即可链接上
```

项目:

recruit.students.war--->java写的编译后的经过打包后的包

recruit_students_sql.sql--->项目所依赖的sql文件,里面是数据库的表和内容



```shell
#1.把war包扔给tomcat的webapps目录即可(前提:tomcat处于启动状态),扔完后会tomcat会自动的解开war包形成一个文件夹
#2.测试:http://linux的ip:8080/加压后形成的文件夹名
#通过1,2步,即可完成界面部署,但这个时候你还登录不上去,因为你没有数据库,根本不知道用户名和密码等信息
#3.打开navicat,链接服务器,右键---新建数据库---student
#4.双击student库,右键----运行sql文件----选择给定的recruit_students_sql.sql文件,即可附加上数据库
#5.进入/usr/java/tomcat8080/webapps/recruit.students下,查找一个叫data的文件,他的后缀是properties.
#6.编辑这个文件中的数据库的相关信息,改成自己服务器的信息即可
#改:ip,端口.数据库名,用户名,密码
#7.保存退出
#8.重启tomcat
#  进入bin,先./shutdown.sh,再./startup.sh
#9.打开浏览器,输入项目网址,用admin/test123即可进入

```

### 3.nginx+tomcat的负载均衡方案





## 5.补充

### 1.tomcat的学习

1.tomcat的目录

bin:核心的sh脚本

​	**startup.sh 启动	shutdown.sh 关闭**

conf: 配置文件

​	**server.xml** 修改端口等

​	tomcat_users.xml 用户和权限(第四点)

​	web.xml(以后你学java的框架时,就会涉及到)

lib:核心内库 library

​	是一些核心的jar包.我工作后不删除即可.我也不轻易的加入其他的jar在里面.(会影响启动速度和冲突)

logs:**日志**

​	最核心的日志:**catalina.out**

​	我们查看日志:tail -f catalina.out

​	上班后,非常常用,我们一般会打开日志,然后界面做个操作后马上看日志,看是否有各种异常出现

​		如:界面操作时没有错误,但看日志发现有异常exception,那么恭喜你,你找到了潜在的bug

​		     界面操作时有错误,马上看日志,可能会有异常,于是我截图异常给开发,辅助他定位问题,如果你看得懂,直接指			 出来到底哪错,甚至还知道怎么改,就更好.而这一切的手法都是看日志得到的

​	  **因此.看日志定位问题,是测试人员以及各种IT人必会**技能.

**webapps**:web applicatiions

​	我们所有开发的项目想让tomcat认识,你就把项目的编译后的包放在webapps下即可



2.修改tomcat的端口

​	进入conf目录,打开server.xml

​	修改开启和关闭端口即可,关闭在22行,开启在69行



3.修改默认项目的文件信息

进入tomcat/webapps/ROOT,编辑index.jsp即可修改默认项目的信息



4.修改用户和权限访问信息(选修)

















