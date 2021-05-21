## 		centos7.6搭建LNMP部署wordpress

**WordPress是一款常用的搭建个人博客网站软件，该软件使用PHP语言开发。本次搭建的系统是centos7.6.下载地址：**<https://www.jianshu.com/p/a63f47e096e8> ,按照指示下载

<http://www.zsythink.net/archives/447/> 

- #### **搭建nginx**

  默认情况下centos7.6没有nginx的源，需要配置Nginx官网提供Gentos的源地址。

  

- ##### **配置nginx源**

```linux
[root@hl-web lnmp-wordpress]# rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm

[root@hl-web ~]# yum search nginx

```



- #### **安装nginx**

```
[root@hl-web ~]#  yum install -y pcre-devel openssl-devel #安装nginx依赖包
[root@hl-web ~]# yum install -y nginx
```



- **配置nginx的/etc/nginx/conf.d/default.conf文件，实现PHP联动**

```
[root@hl-web ~]# vim /etc/nginx/conf.d/default.conf
打开文件后将下面的内容复制到default.conf里

server {
 #访问localhost这个网址成功时执行
 
 listen       80;				#监听端口号
 root   /usr/share/nginx/html;	 #页面展示的文件所在文件夹
 server_name  localhost;		 #访问的网址
 #charset koi8-r;
 #access_log  /var/log/nginx/log/host.access.log  main;
 #
 location / {
         index index.php index.html index.htm;  #具体访问的文件，在这里面找
 }

 #下面是访问网址失败时执行的

 #error_page  404              /404.html;
 #redirect server error pages to the static page /50x.html
 #
 error_page   500 502 503 504  /50x.html;
 location = /50x.html {
     root   /usr/share/nginx/html;
 }
 #pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
 #
 location ~ .php$ {
     fastcgi_pass   127.0.0.1:9000;
     fastcgi_index  index.php;
     fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
     include        fastcgi_params;
  }
}
```



- **添加域名**(将localhost添加到可访问的网址里)

  需要修改配置文件，将localhost写入文件里

  ```
  [root@hl-web ~]# vim /etc/hosts
  ```

  修改后的内容如下：

  ```
  127.0.0.1 localhost
  ```

  

- **启动nginx并设置开机自启**

  ```
  [root@hl-web ~]# systemctl start nginx       #启动nginx服务
  [root@hl-web ~]# systemctl enable nginx 	 #设置linux开机自动启动nginx
  ```

  

- **检测nginx是否配置成功**

  在虚拟机的浏览器地址栏里输入网址127.0.0.1访问nginx，查看是否配置成功

  当输入localhost时 展示的页面应该是/usr/share/nginx/html/index.html

  **成功页面：**

  

  

  ![1564565836426](C:\Users\EDZ\AppData\Local\Temp\1564565836426.png)







- **任务：nginx上面挂两个域名并且能够通过域名访问**

  - **思路**：上面已经添加了一个域名：localhost，在添加两个写的代码与上面相似,这次我们将两个域名放在不同的文件夹，通过对比让你更好理解代码

  - **首先修改/etc/nginx/conf.d/default.conf**

    ```
    [root@hl-web ~]# vim /etc/nginx/conf.d/default.conf
    ```

    修改后的内容为：

    - ```
      server {
       #访问localhost这个网址成功时执行
       
       listen       80;				#监听端口号
       root   /usr/share/nginx/html;	 #页面展示的文件所在文件夹
       server_name  localhost;		 #访问的网址
       #charset koi8-r;
       #access_log  /var/log/nginx/log/host.access.log  main;
       #
       location / {
               index index.html;  	#具体访问的文件
       }
      
       #下面是访问网址失败时执行的
      
       #error_page  404              /404.html;
       #redirect server error pages to the static page /50x.html
       #
       error_page   500 502 503 504  /50x.html;
       location = /50x.html {
           root   /usr/share/nginx/html;
       }
       #pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
       #
       location ~ .php$ {
           fastcgi_pass   127.0.0.1:9000;
           fastcgi_index  index.php;
           fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
           include        fastcgi_params;
        }
      }
      
      
      #www.hl02.com
      server {
          listen       80;
          root   /usr/share/nginx/html/hl02;
          server_name  www.hl02.com;
          #charset koi8-r;
          #access_log  /var/log/nginx/log/host.access.log  main;
                
          location / {
                  index hl02.html;
          }              
      }     
      
      #www.hl01.com
      server {
          listen       80; 
          root   /usr/share/nginx/html/hl01;
          server_name  www.hl01.com;
          #charset koi8-r;
          #access_log  /var/log/nginx/log/host.access.log  main;
          
          location / {
                  index hl01.html;   
          }
      }
      ```

- **然后接下来要把新加入的域名添加到/ect/hosts里**

  ```
  [root@hl-web ~]# vim /etc/hosts
  ```

  修改后内容为：

  ```
  127.0.0.1 localhost www.hl01.com www.hl02.com
  ```

- **最后一步创建域名对应的站点目录及文件，也就是要写新的展示页面html文件**

  ```
  [root@hl-web ~]# cd /usr/share/nginx/html/
  [root@hl-web html]# mkdir hl01
  [root@hl-web hl01]# echo "我是www.hl01.com">>hl01.html
  [root@hl-web html]# mkdir hl02
  [root@hl-web html]# cd hl02
  [root@hl-web hl02]# echo "我是www.hl02.com">> hl02.html
  ```

- **重启nginx服务**

  ```
  [root@hl-web hl01]# systemctl restart nginx
  ```

  

- **验证域名是否添加成功**

  在浏览器地址栏输入新添加的域名 看展示出来的是否是对应的html页面



- #### **搭建PHP**

  - 配置PHP源

    ```
    [root@hl-web ~]# rpm -Uvh https://mirrors.cloud.tencent.com/epel/epel-release-latest-7.noarch.rpm
    [root@hl-web ~]# rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
    ```

  - 安装PHP-fpm所属需要的包

    ```
    [root@hl-web ~]# yum -y install mod_php72w.x86_64 php72w-cli.x86_64 php72w-common.x86_64 php72w-mysqlnd php72w-fpm.x86_64
    ```

  - 启动PHP-fpm并设置开机自启

    ```
    [root@hl-web ~]# systemctl start php-fpm.service
    [root@hl-web ~]# systemctl enable php-fpm.service
    ```

  - 验证php-nginx环境配置

    ```
    [root@hl-web ~]# echo "<?php phpinfo(); ?>" > /usr/share/nginx/html/index.php
    ```

    浏览器中输入http://127.0.0.1/index.php，页面显示如下，则说明PHP-Nginx环境配置成功

    ![1564567398851](C:\Users\EDZ\AppData\Local\Temp\1564567398851.png)

- #### **安装mariadb**

  - 查看系统是否有mariadb

  ```
  [root@hl-web ~]# rpm -qa | grep -i mariadb
  ```

  - 删除mariadb现有的包

  ```
  [root@hl-web ~]# yum remove mariadb-libs.x86_64
  ```

  - 配置mariadb源

  ```
  [root@hl-web ~]# vim /etc/yum.repos.d/MariaDB.repo
  ```

  ​	修改后的内容为：

  ```
  # MariaDB 10.4 CentOS7-amd64
  [mariadb]
  name = MariaDB
  baseurl = http://mirrors.cloud.tencent.com/mariadb/yum/10.4/centos7-amd64/
  gpgkey = http://mirrors.cloud.tencent.com/mariadb/yum/RPM-GPG-KEY-MariaDB
  gpgcheck=1
  ```

  ​	然后再执行：

  ```
  [root@hl-web ~]# yum clean all
  ```

  

  - **安装mariadb**

    ```
    [root@hl-web ~]# yum -y install MariaDB-client MariaDB-server
    ```

  - **启动mariadb并设置开机自启**

    ```
    [root@hl-web ~]# systemctl start mariadb.service
    [root@hl-web ~]# systemctl enable mariadb
    ```

  - **设置mariadb的root密码及基础配置**

    ```
    [root@hl-web ~]# mysql_secure_installation 
    ```

  - **会出现下面的界面，依次按照步骤执行 ,没有y的直接按回车**

    ![1564568113745](C:\Users\EDZ\AppData\Local\Temp\1564568113745.png)

    

    

  - **登陆mariadb，测试是否安装成功**

    ![1564568285475](C:\Users\EDZ\AppData\Local\Temp\1564568285475.png)

  

  

  

  

- #### **安装wordpress**

  - 删除网站根目录下的index.php测试文件

  ```
  [root@hl-web html]#
  ```

  - WordPress官方网站下载WorldPress-5.0.4中文版本

    下载地址：<https://wordpress.org/download/> 

    可以在windows下下载，然后拖到虚拟机里，将该文件放到/usr/share/nginx/html目录下并解压

  ```
  [root@hl-web html]# tar zxvf wordpress-5.0.4-zh_CN.tar.gz
  ```

  - 配置数据库

    - 创建wordpresss数据库

    ```
    [root@hl-web html]# mysql -u root -p
    MariaDB [(none)]> create database wordpress;
    Query OK, 1 row affected (0.001 sec)
    ```

    - 创建wordpress用户并设置密码

    ```
    MariaDB [(none)]> CREATE USER 'username'@'host' IDENTIFIED BY 'password';
    ```

    > 说明：

    > username：你将创建的用户名

    > host：指定该用户在哪个主机上可以登陆，如果是本地用户可用localhost，如果想让该用户可以**从任意远程主机登陆**，可以使用通配符`%`

    > password：该用户的登陆密码，密码可以为空，如果为空则该用户可以不需要密码登陆服务器

    - 给用户授权

      ```
      GRANT ALL ON *.* TO 'username'@'host';
      ```

      

- **写入数据库信息**

  - 进入 WordPress 安装目录，将wp-config-sample.php文件复制到wp-config.php文件中，并将原先的示例配置文件保留作为备份

    ```
    [root@hl-web html]# cd wordpress/
    [root@hl-web wordpress]# cp wp-config-sample.php wp-config.php
    ```

  - 打开wp-config.php,将已配置好的数据库相关信息写入

    ```
    [root@hl-web wordpress]# vim wp-config.php
    /** WordPress数据库的名称 */
    define('DB_NAME', 'wordpress');
    
    /** MySQL数据库用户名 */
    define('DB_USER', 'username');
    
    /** MySQL数据库密码 */
    define('DB_PASSWORD', 'password');
    
    /** MySQL主机 */
    define('DB_HOST', '127.0.0.1');
    
    /** 创建数据表时默认的文字编码 */
    define('DB_CHARSET', 'utf8');
    
    /** 数据库整理类型。如不确定请勿更改 */
    define('DB_COLLATE', '');
    ```

  - **验证wordpress，浏览器输入http://127.0.0.1/wordpress**

![1564569464101](C:\Users\EDZ\AppData\Local\Temp\1564569464101.png)

- **安装wordpress**

![1564569480712](C:\Users\EDZ\AppData\Local\Temp\1564569480712.png)

![1564569491226](C:\Users\EDZ\AppData\Local\Temp\1564569491226.png)

- **搭建成功，登陆到wordpress**

![1564569521024](C:\Users\EDZ\AppData\Local\Temp\1564569521024.png)

![1564569528249](C:\Users\EDZ\AppData\Local\Temp\1564569528249.png)

