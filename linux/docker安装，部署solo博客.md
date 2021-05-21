#### docker安装：

安装需要的软件包， yum-util 提供yum-config-manager功能，另外两个是devicemapper驱动依赖的 

```
yum install -y yum-utils device-mapper-persistent-data lvm2
```



设置yum源 

```
 yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```



可以查看所有仓库中所有docker版本，并选择特定版本安装 

```
yum list docker-ce --showduplicates | sort -r
```



安装Docker，命令：yum install docker-ce-版本号，我选的是17.12.1.ce，如下 

```
 yum install docker-ce-17.12.1.ce
```



启动Docker，命令：systemctl start docker，然后加入开机启动，如下 

```
systemctl start docker
systemctl enable docker
```



验证安装是否成功(有client和service两部分表示docker安装启动都成功了) 

```
docker version 
```





### 部署solo博客 



#### 获取最新镜像

```
docker pull b3log/solo
```



#### 查看镜像

```
docker images
```



#### 启动容器

- 使用 MySQL(这里你的root用户要可以远程连接)

  可以进入mysql查看

  use mysql;

  select user,host from user;

  查看你的用户和端口，如果root不是%,你要进行修改

  update host='%' from user where user='root';

  刷新权限：

  flush privileges;

  先手动建库（库名 `solo`，字符集使用 `utf8mb4`，排序规则 `utf8mb4_general_ci`），然后启动容器：

  ```
  创库：
  mysql -uroot -p
  password
  
  create database solo character set 'utf8mb4' collate 'utf8mb4_general_ci';
  
  exit
  
  创建容器：
  docker run --detach --name solo --network=host  -e "SERVER_NAME=www.hl66.com" -e "SERVER_PORT=80" -e "SERVER_SCHMEA=http" --env RUNTIME_DB="MYSQL" --env JDBC_USERNAME="root" --env JDBC_PASSWORD="password" --env JDBC_DRIVER="com.mysql.cj.jdbc.Driver" --env JDBC_URL="jdbc:mysql://192.168.233.129:3306/solo?useUnicode=yes&characterEncoding=UTF-8&useSSL=false&serverTimezone=UTC" b3log/solo --listen_port=8080 --server_host=192.168.233.129
  ```

- 可以查看docker运行的容器

```
docker ps -q
```

- 验证是否成功

  输入网址 192.168.233.130:8080







#### 



