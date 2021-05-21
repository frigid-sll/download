### centos7下zabbix安装与部署

学习：<https://www.linuxidc.com/Linux/2018-08/153665.htm> 

#### 1、Zabbix介绍

- zabbix是一个基于WEB界面的提供分布式系统监视以及网络监视功能的企业级的开源解决方案。
- zabbix能监视各种网络参数，保证服务器系统的安全运营；并提供灵活的通知机制以让系统管理员快速定位/解决存在的各种问题。
- zabbix由2部分构成，zabbix server与可选组件zabbix agent。
- zabbix server可以通过SNMP，zabbix agent，ping，端口监视等方法提供对远程服务器/网络状态的监视，数据收集等功能，它可以运行在Linux，Solaris，HP-UX，AIX，Free BSD，Open BSD，OS X等平台上。

 

#### 2、LAMP/LNMP介绍

- LAMP：Linux+Apache+Mysql/MariaDB+Perl/PHP/Python一组常用来搭建动态网站或者服务器的开源软件，本身都是各自独立的程序，但是因为常被放在一起使用，拥有了越来越高的兼容度，共同组成了一个强大的Web应用程序平台。
- LNMP：LNMP指的是一个基于CentOS/Debian编写的Nginx、PHP、MySQL、phpMyAdmin、eAccelerator一键安装包。可以在VPS、独立主机上轻松的安装LNMP生产环境。
- L：linux
- A：apache
- N：nginx
- M：mysql,mariaDB
- P：php,python,perl



#### 3、Zabbix的安装

```
关闭SeLinux(选哪个都行)

临时关闭：setenforce 0
永久关闭：vi /etc/selinux/config 
```

```
关闭防火墙(选哪个都行)

1、临时关闭:systemctl stop firewalld.service
2、永久关闭:systemctl disable firewalld.service
```



- **安装环境**

  #### LAMP

  - 安装apache

    ```
    yum install -y httpd
    ```

    ![1564572067562](C:\Users\EDZ\AppData\Local\Temp\1564572067562.png)

  - httpd服务开机进行自启 

    ```
    systemctl enable httpd
    ```

  - 启动httpd服务

    ```
    systemctl start httpd
    ```

    ![1564572132334](C:\Users\EDZ\AppData\Local\Temp\1564572132334.png)

  - 接下来是安装数据库 mariadb请看搭建wordpress

- 安装php环境  

  ```
  yum install -y php php-mysql
  ```

  

- 安装zabbix

  - 下载包

    ```
    rpm -ivh http://repo.zabbix.com/zabbix/3.4/rhel/7/x86_64/zabbix-release-3.4-2.el7.noarch.rpm
    ```

    

  - 安装zabbix的包

    ```
    yum install -y zabbix-server-mysql zabbix-get zabbix-web zabbix-web-mysql zabbix-agent zabbix-sender
    ```

  - 创建一个zabbix库并设置为utf8的字符编码格式 

    ```
    create database zabbix character set utf8 collate utf8_bin;
    ```

  - 创建账户并且授权设置密码(给来自loclhost的用户zabbxi分配可对数据库zabbix所有表进行所有操作的权限，并且设定密码为zabbix )

    ```
    grant all privileges on zabbix.* to zabbix@localhost identified by 'zabbix';
    ```

  - 刷新 

    ```
    flush privileges;
    ```

  - exit退出

- 导入表，切换到此目录下

  ```
  cd /usr/share/doc/zabbix-server-mysql-3.2.10/
  ```

- 进行解压

  ```
  gunzip create.sql.gz
  ```

- 对表进行导入 

  ```
  依次执行命令：
  mysql
  use zabbix;
  source create.sql
  ```

- 配置zabbix server配置文件

  配置文件目录

  ```
  cd /etc/zabbix
  ```

- 对zabbix_server.conf进行配置

  ```
  vi zabbix_server.conf
  ```

  修改内容如下图：

  ![1564572691383](C:\Users\EDZ\AppData\Local\Temp\1564572691383.png)

  ![1564572700943](C:\Users\EDZ\AppData\Local\Temp\1564572700943.png)

  ![1564572706926](C:\Users\EDZ\AppData\Local\Temp\1564572706926.png)

  ![1564572712134](C:\Users\EDZ\AppData\Local\Temp\1564572712134.png)

  ![1564572716551](C:\Users\EDZ\AppData\Local\Temp\1564572716551.png)

  

- 运行zabbix-server服务,开机自启zabbix-server服务

```
systemctl start zabbix-server.service
systemctl enable zabbix-server.service
```

- 配置php

```
cd /etc/httpd/conf.d
vi zabbix.conf
systemctl restart httpd.service
```

![1564572845286](C:\Users\EDZ\AppData\Local\Temp\1564572845286.png)

- 登陆zabbix网址设置 :你的ip网址/zabbix

- ![1564572902872](C:\Users\EDZ\AppData\Local\Temp\1564572902872.png)

- ![1564572909975](C:\Users\EDZ\AppData\Local\Temp\1564572909975.png)

- **password是我们设置的数据库密码zabbix** 

- ![1564572930865](C:\Users\EDZ\AppData\Local\Temp\1564572930865.png)

- ![1564572944560](C:\Users\EDZ\AppData\Local\Temp\1564572944560.png)

- ![1564572951437](C:\Users\EDZ\AppData\Local\Temp\1564572951437.png)

- ![1564572957600](C:\Users\EDZ\AppData\Local\Temp\1564572957600.png)

- **登陆账户是Admin**

  **密码是zabbix**



- ![1564572981099](C:\Users\EDZ\AppData\Local\Temp\1564572981099.png)

- 设置中文

   

- ![1564572997630](C:\Users\EDZ\AppData\Local\Temp\1564572997630.png)

- ![1564573005426](C:\Users\EDZ\AppData\Local\Temp\1564573005426.png)

- 对服务器自身进行监控 

- ![1564573019582](C:\Users\EDZ\AppData\Local\Temp\1564573019582.png)

- 解决中文乱码无法显示的问题

  ​			 ![1564573035079](C:\Users\EDZ\AppData\Local\Temp\1564573035079.png)

  ![1564573040969](C:\Users\EDZ\AppData\Local\Temp\1564573040969.png)

  **从我们电脑win7里面找到黑体右键复制到桌面然后拉到zabbix服务器上面**

  **直接修改字体名字**

  **切换到这个目录下面: /usr/share/zabbix/fonts**

- ![1564573065128](C:\Users\EDZ\AppData\Local\Temp\1564573065128.png)

- **现在的中文字体是显示正常的了** 

- ![1564573078329](C:\Users\EDZ\AppData\Local\Temp\1564573078329.png)

- 