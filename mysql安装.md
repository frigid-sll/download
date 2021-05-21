### windows下安装mysql-8.0

直接下载：<https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-8.0.11-winx64.zip> 

#### 安装

##### 　　1.1，解压zip包到安装目录

　　比如我的安装目录是：D:\mysql-8.0.11-winx64

##### 　　1.2，配置文件

　　在Windows系统中，配置文件默认是安装目录下的 my.ini 文件（或my-default.ini），部分配置需要在初始安装时配置，大部分也可以在安装完成后进行更改。当然，极端情况下，所有的都是可以更改的。

　　我们发现解压后的目录并没有my.ini文件，没关系可以自行创建。在安装根目录下添加 my.ini，比如我这里是：D:\mysql-8.0.11-winx64\my.ini，写入基本配置：

```
[mysqld]

#设置3306端口

port=3306

#设置mysql的安装目录

basedir=D:\\ROUTE\\mysql8   # 此处可以用单斜杠也可以用双斜杠，有的人用单斜杠会错，自己试试就知道了

#设置mysql数据库的数据的存放目录

datadir=D:\mysql-8.0.11-winx64\Data   # 此处同上

#允许最大连接数

max_connections=200

#允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统

max_connect_errors=10

#服务端使用的字符集默认为UTF8

character-set-server=utf8

#创建新表时将使用的默认存储引擎

default-storage-engine=INNODB

#默认使用“mysql_native_password”插件认证

default_authentication_plugin=mysql_native_password

[mysql]

#设置mysql客户端默认字符集

default-character-set=utf8

[client]

#设置mysql客户端连接服务端时默认使用的端口，可能和VMware的端口冲突，可自行修改

port=3306

default-character-set=utf8

[WinMySQLAdmin]
Server=D:\mysql-8.0.11-winx64\bin\mysqld.exe	

```



**配置环境变量**

D:\mysql-8.0.11-winx64\bin

**以管理员身份进入cmd**

进入D:\mysql-8.0.11-winx64\bin该目录下

```
mysqld --initialize --console 
```



执行完成后，会打印 root 用户的初始默认密码

其中root@localhost:后面的“rI5rvf5x5G,E”就是初始密码 

```
mysqld --install
net start mysql
```







### linux下安装mysql-5.7

#### 1 下载并安装MySQL官方的 Yum Repository

```
[root@localhost ~]# wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
```

  使用上面的命令就直接下载了安装用的Yum Repository，大概25KB的样子，然后就可以直接yum安装了。

```
[root@localhost ~]# yum -y install mysql57-community-release-el7-10.noarch.rpm
```

  之后就开始安装MySQL服务器。

```
[root@localhost ~]# yum -y install mysql-community-server
```

  这步可能会花些时间，安装完成后就会覆盖掉之前的mariadb。

![img](https://images2017.cnblogs.com/blog/1079354/201707/1079354-20170726201927328-459165254.png)

至此MySQL就安装完成了，然后是对MySQL的一些设置。

#### 2 MySQL数据库设置

  首先启动MySQL

```
[root@localhost ~]# systemctl start  mysqld.service
```

  查看MySQL运行状态，运行状态如图：

```
[root@localhost ~]# systemctl status mysqld.service
```

![img](https://images2017.cnblogs.com/blog/1079354/201707/1079354-20170726202441687-1168874203.png)

  此时MySQL已经开始正常运行，不过要想进入MySQL还得先找出此时root用户的密码，通过如下命令可以在日志文件中找出密码：

```
[root@localhost ~]# grep "password" /var/log/mysqld.log
```

![img](https://images2017.cnblogs.com/blog/1079354/201707/1079354-20170726202722796-1932560887.png)

  如下命令进入数据库：

```
[root@localhost ~]# mysql -uroot -p
```

密码有安全限制。可以通过如下命令修改：

```
mysql> set global validate_password_policy=0;
mysql> set global validate_password_length=1;
```

然后可以改密码了

```
set password='new password'
```

设置之后就是我上面查出来的那几个值了，此时密码就可以设置的很简单，例如1234之类的。到此数据库的密码设置就完成了。

  但此时还有一个问题，就是因为安装了Yum Repository，以后每次yum操作都会自动更新，需要把这个卸载掉：

```
[root@localhost ~]# yum -y remove mysql57-community-release-el7-10.noarch
```

 此时才算真的完成了。 