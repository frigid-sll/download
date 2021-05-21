#### 安装node.js

```
# 下载源码：
$ wget https://nodejs.org/download/release/v6.0.0/node-v6.0.0.tar.gz
$ tar -zvxf node-v6.0.0.tar.gz
$ cd node-v6.0.0
$ ./configure
#NOTE: 这里需要使用python2.7 的环境。python版本相关的问题，可以阅读python版本管理(python)相关的内容。

$ make
#NOTE: 这个比较费时间。 

$ make install 

$ node --version
v6.0.0

一、升级方法:
1.产看node版本，没安装的请先安装；
$ node -v

2.清楚node缓存；
$ sudo npm cache clean -f

3.安装node版本管理工具'n';
$ sudo npm install n -g

4.使用版本管理工具安装指定node或者升级到最新node版本；
$ sudo n stable （安装node最新版本）
或安装指定版本
$ sudo n （可以安装node指定版本 sudo n 10.10.0）

5.使用node -v查看node版本，如果版本号改变为你想要的则升级成功。

```
