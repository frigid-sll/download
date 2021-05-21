#### 安装python

```
wget https://www.python.org/ftp/python/3.6.2/Python-3.6.2.tar.xz 下载安装包
yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel gcc   安装依赖包 
tar -Jxvf Python-3.6.2.tar.xz  解压tar包
cd Python-3.6.1 切换到Python路径下
./configure prefix=/usr/local/python3 进行安装配置
make && make install 编译和编译安装
ln -s /usr/local/python3/bin/python3  /usr/bin/python3 对python3 进行一个软连接
ln -s  /usr/local/python3/bin/pip3  /usr/bin/pip3 对pip3 命令进行一个软连接
pip3 install --upgrade pip
pip3 install sqlalchemy  配置完成，顺带测试
pip3 install pymysql
```



#### 安装`node.js`

```
# 下载源码：
$ wget https://nodejs.org/download/release/v6.0.0/node-v6.0.0.tar.gz
$ tar -zvxf node-v6.0.0.tar.gz
$ cd node-v6.0.0
$ ./configure

$ make
#NOTE: 这个比较费时间。 

$ make install 

$ node --version
v6.0.0

```



#### 安装`vue`

```
npm install vue-cli
```



##### `netstat` 查看运行的服务

```
netstat -nptl 
```



##### `fuser` 杀死8000端口号的进程

```
fuser -k 8000/tcp
```



#### 部署`django`环境，导出`package.txt`

```
pip3 install -r package.txt
```

- `package.txt`内容

```
amqp==1.4.9
anyjson==0.3.3
Babel==2.7.0
billiard==3.3.0.23
celery==3.1.26.post2
certifi==2018.8.24
chardet==3.0.4
Django==2.1.8
django-celery==3.2.2
django-ckeditor==5.7.1
django-filter==2.2.0
django-js-asset==1.2.2
django-redis==4.10.0
djangorestframework==3.10.2
flower==0.9.3
idna==2.8
kombu==3.0.37
Markdown==3.1.1
Pillow==6.1.0
pycryptodome==3.8.2
pycryptodomex==3.7.2
PyMySQL==0.9.3
python-alipay-sdk==1.10.1
pytz==2019.1
redis==2.10.6
requests==2.22.0
sqlparse==0.3.0
tornado==5.1.1
urllib3==1.25.3
wincertstore==0.2
datetime
rsa
django-cors-headers
```

- 运行服务

```
在settings.py中需要
将name参数用str()进行转换
DATABASES = {    
	'default': {       
    	'ENGINE': 'django.db.backends.sqlite3',        
    	'NAME': str(BASE_DIR / 'db.sqlite3'),    
    	}
    }
    
python3 manage.py runserver
```





#### 配置安装`uwsgi`

```
pip3 install uwsgi
```

- 配置软连接

```
ln -s /usr/local/python3/bin/uwsgi /usr/bin/uwsgi
```

- 使用`uwsgi`脚本运行`django`项目。创建脚本`script`目录

```
mkdir script
cd script
```

`目录`

>`dj`						//`django`项目
>
>>`db.sqlite3`    //数据库文件
>>
>>`FinanceSdkDemo`   	//`c++`目录
>>
>>`myapp` 					//`django`项目`app`
>>
>>`script`					//`uwsgi`脚本目录
>>
>>`vue	`						//`vue`目录
>>
>>`wfastcgi.py	`			//部署`IIS`需要的`py`文件
>>
>>`dist	`						//打包`vue`的静态文件目录
>>
>>`manage.py`
>>
>>`myproject`
>>
>>`static`					//真正用到的静态文件目录
>>
>>`web.config`

- 写入脚本

```
vim uwsgi.ini
内容：
[uwsgi]
chdir=/root/桌面/dj			#项目目录
module=myproject.wsgi			#指定项目的application
socket=/root/桌面/dj/script/uwsgi.sock		#指定sock的文件路径
workers=5						#进程个数
pidfile=/root/桌面/dj/script/uwsgi.pid		#指定pid的文件路径
http=192.168.0.69:8099			#指定IP端口
static-map=/static=/root/桌面/dj/static		 #指定静态文件
uid=root		#用户
gid=root		#组
master=true		#启用主进程
vacuum=true		#自动移除unix Socket和pid文件当服务停止的时候
enable-threads=true		#启用线程
thunder-lock=true 		#序列化接受的内容，如果可能的话
harakiri=30 			#设置自中断时间
post-buffering=4096 	#设置缓冲
daemonize=/root/桌面/dj/script/uwsgi.log 	#设置日志目录
```

- 启动脚本

```
uwsgi --ini uwsgi.ini
```

- 启动完成

```
[root@sll script]# ls
uwsgi.ini  uwsgi.log  uwsgi.pid  uwsgi.sock
```



#### 配置安装`nginx`

- 下载`nginx`

```
wget -c https://nginx.org/download/nginx-1.12.2.tar.gz
```

- 解压包

```
tar -zxvf nginx-1.12.2.tar.gz
```

- 编译安装

```
cd nginx-1.12.2
./configure
make && make install
```

- 创建软连接

```
ln -s /usr/local/nginx/sbin/nginx /usr/bin/nginx
```

- 启动`nginx`(默认端口80，如果80端口被占用需要先停止80端口)

```
fuser -k 80/tcp		#停止80端口的使用
nginx				#启动nginx
```

- 备份配置文件，【防止错误先备份一份】

```
[root@sll nginx-1.12.2]# cd conf
[root@sll conf]# cp nginx.conf nginx.conf.bak
```

- 创建`Error_log`路径(`/var/log/nginx`)

```
mkdir nginx
cd nginx
touch error.log
```

- 修改配置文件

```
vim nginx.conf
```

```
http {
    include       mime.types;
    default_type  application/octet-stream;

	#这里规定了日志的格式，默认是注释的，我们需要解开注释
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80;	 #监听端口
        server_name  localhost;		#服务名称

        charset utf-8;		#服务器编码

        access_log  /var/log/nginx/access.log  main;		 #访问日志路径

        gzip_types text/plain application/x-javascript text/css text/javascript application/x-httpd-php application/json text/json image/jpeg image/gif image/png application/octet-stream; #压缩格式

        error_log /var/log/nginx/error.log error;		#错误日志注意

        location / {
                include uwsgi_params;		#nginx加载uwsgi模块
                uwsgi_connect_timeout 30;		#连键超时时间
                uwsgi_pass unix:/root/桌面/dj/script/uwsgi.sock;		 #nginx对应的uwsgi socket文件
        }

        location = /static/ {
            alias /root/桌面/dj/static;  #静态文件路径
            index index.html index.htm;  #首页
            }

         

```



- 杀掉进程，重新启动

```
pkill -9 uwsgi
pkill -9 nginx
uwsgi --ini uwsgi.ini 	#必须在本文件路径下
nginx
```

