[![博客园Logo](https://www.cnblogs.com/images/logo.svg?v=R9M0WmLAIPVydmdzE2keuvnjl-bPR7_35oHqtiBzGsM)](https://www.cnblogs.com/)[首页](https://www.cnblogs.com/)[新闻](https://news.cnblogs.com/)[博问](https://q.cnblogs.com/)[专区](https://brands.cnblogs.com/)[闪存](https://ing.cnblogs.com/)[班级](https://edu.cnblogs.com/)![搜索](https://www.cnblogs.com/images/aggsite/search.svg)[注册](https://account.cnblogs.com/signup/)[登录](javascript:void(0);)

[小丞cc](https://www.cnblogs.com/zfcblog/)

- [博客园](https://www.cnblogs.com/)
- [首页](https://www.cnblogs.com/zfcblog/)
- [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
- [联系](https://msg.cnblogs.com/send/小丞cc)
- [订阅](javascript:void(0))
- [管理](https://i.cnblogs.com/)

随笔 - 11 文章 - 1 评论 - 0 阅读 - 5933

# [Linux之CentOS 7镜像下载（附带安装教程）](https://www.cnblogs.com/zfcblog/p/13582659.html)

CentOS 7镜像下载

官网下载链接：http://isoredirect.centos.org/centos/7/isos/x86_64/

step1: 进入下载页，选择阿里云站点进行下载

Actual Country 国内资源 Nearby Countries 周边国家资源

阿里云站点：http://mirrors.aliyun.com/centos/7/isos/x86_64/

每个链接都包括了镜像文件的地址、类型及版本号等信息

选择当前国家资源区站点下载，获取资源速度比较快

step1: 进入阿里云站点，选择 CentOS-7-x86_64-DVD-1804.iso下载

各个版本的ISO镜像文件说明（文件名的格式一致的即可，更新版本后文件名会边）：

CentOS-7-x86_64-DVD-1708.iso 标准安装版（推荐）

CentOS-7-x86_64-Everything-1708.iso 完整版，集成所有软件（以用来补充系统的软件或者填充本地镜像）

CentOS-7-x86_64-LiveGNOME-1708.iso GNOME桌面版

CentOS-7-x86_64-LiveKDE-1708.iso KDE桌面版

CentOS-7-x86_64-Minimal-1708.iso 精简版，自带的软件最少

CentOS-7-x86_64-NetInstall-1708.iso 网络安装版（从网络安装或者救援系统）

 

# CentOS7安装教程

## 1. 新建虚拟机

点击“创建新的虚拟机”

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625170455942.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

点击“下一步”

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020062517051750.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

选择“稍后安装操作系统”，点击“下一步”

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625170537165.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)
选择"CentOS 7 64"，点击“下一步”

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625170555542.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

起一个虚拟机名字，设置一个合适的安装位置，点击“下一步”

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625170640339.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

点击“下一步”

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625170714751.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

点击“自定义硬件”，配置如下图：内存2G、cpu1个8核、移除声卡打印机U盘、桥接模式、添加iso镜像，最后点击关闭。

![img](https://img2020.cnblogs.com/blog/1939709/202008/1939709-20200829153314353-1687043374.png)

 

 

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625170736337.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

点击关闭后，点击“完成”

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625170752810.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

## 2. 配置虚拟机

点击“开启此虚拟机”

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625170809135.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)
选择“Install centOS 7”，按下Enter键
![在这里插入代码片](https://img-blog.csdnimg.cn/20200625170832228.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

选择语言“简体中文”

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625170913136.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入代码片](https://img-blog.csdnimg.cn/20200625170939231.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)
点击“安装源”，双击“完成”即可

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625171017863.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

点击“软件选择”，选择“带GUI的服务器+开发工具”如下，双击“完成”

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625171059845.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

点击“安装位置”，双击“完成”【生产环境中最好是选择“我要配置分区”，我这里物理硬盘不大，就自动配置分区了。】

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625171227230.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)
点击“网络和主机名”,修改主机名，并开启以太网

![img](https://img2020.cnblogs.com/blog/1939709/202008/1939709-20200829161619757-24822107.png)

 

 

选择完后，点击“开始安装”

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625171310196.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

设置root用户密码并创建一个普通用户
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625171347337.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625171440909.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625171507814.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

等待安装完成。

点击“重启”
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625171547955.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

授权许可证，点击“完成配置”
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625171628497.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

等待开机，安装完成如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625171700559.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

点击“未列出”，以root用户登录，进行初始化配置，显示如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200625171757594.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNjUyMjA5OQ==,size_16,color_FFFFFF,t_70#pic_center)

[好文要顶](javascript:void(0);) [关注我](javascript:void(0);) [收藏该文](javascript:void(0);) [![img](https://common.cnblogs.com/images/icon_weibo_24.png)](javascript:void(0);) [![img](https://common.cnblogs.com/images/wechat.png)](javascript:void(0);)

[![img](https://pic.cnblogs.com/face/sample_face.gif)](https://home.cnblogs.com/u/zfcblog/)

[小丞cc](https://home.cnblogs.com/u/zfcblog/)
[关注 - 0](https://home.cnblogs.com/u/zfcblog/followees/)
[粉丝 - 1](https://home.cnblogs.com/u/zfcblog/followers/)

[+加关注](javascript:void(0);)

1

0

[« ](https://www.cnblogs.com/zfcblog/p/13574066.html)上一篇： [Django项目中把原生sqlite数据迁移至mysql数据库](https://www.cnblogs.com/zfcblog/p/13574066.html)
[» ](https://www.cnblogs.com/zfcblog/p/13583704.html)下一篇： [Linux中提示没有pip命令解决办法](https://www.cnblogs.com/zfcblog/p/13583704.html)

posted @ 2020-08-29 16:42 [小丞cc](https://www.cnblogs.com/zfcblog/) 阅读(2107) 评论(0) [编辑](https://i.cnblogs.com/EditPosts.aspx?postid=13582659) [收藏](javascript:void(0))





[刷新评论](javascript:void(0);)[刷新页面](https://www.cnblogs.com/zfcblog/p/13582659.html#)[返回顶部](https://www.cnblogs.com/zfcblog/p/13582659.html#top)

登录后才能查看或发表评论，立即 [登录](javascript:void(0);) 或者 [逛逛](https://www.cnblogs.com/) 博客园首页

[【推荐】玩转开发板：旧键盘+OpenHarmony 变身蓝牙键盘 v0.1](https://brands.cnblogs.com/huawei)
[【推荐】大型组态、工控、仿真、CAD\GIS 50万行VC++源码免费下载!](http://www.uccpsoft.com/index.htm)
[【推荐】阿里云爆品销量榜单，精选爆款产品低至0.55折](https://www.aliyun.com/activity/daily/bestoffer?userCode=swh7dvlt)
[【推荐】限时秒杀！国云大数据魔镜，企业级云分析平台](http://www.moojnn.com/?source=bokeyuan)

**园子动态**：
· [致园友们的一封检讨书：都是我们的错](https://www.cnblogs.com/cmt/p/14585828.html)
· [数据库实例 CPU 100% 引发全站故障](https://www.cnblogs.com/cmt/p/14595262.html)
· [发起一个开源项目：博客引擎 fluss](https://www.cnblogs.com/cmt/p/14217355.html)

**最新新闻**：
· [水滴美股上市首日跌近20%，已全力转型“卖保险”](https://news.cnblogs.com/n/693395/)
· [广东一辆特斯拉追尾货车驾驶员当场丧生 官方通报：事故原因调查中](https://news.cnblogs.com/n/693394/)
· [折叠屏iPhone渲染图曝光：左右对折、可秒变掌上电脑](https://news.cnblogs.com/n/693393/)
· [美股周五：道指再创新高 特斯拉止跌反弹涨1.3%](https://news.cnblogs.com/n/693392/)
· [火星车录下火星直升机飞行声音，风声里夹着嗡嗡响](https://news.cnblogs.com/n/693391/)
» [更多新闻...](https://news.cnblogs.com/)

### 公告

昵称： [小丞cc](https://home.cnblogs.com/u/zfcblog/)
园龄： [1年2个月](https://home.cnblogs.com/u/zfcblog/)
粉丝： [1](https://home.cnblogs.com/u/zfcblog/followers/)
关注： [0](https://home.cnblogs.com/u/zfcblog/followees/)

[+加关注](javascript:void(0))

| [<](javascript:void(0);)2021年5月[>](javascript:void(0);) |      |      |      |      |      |      |
| --------------------------------------------------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| 日                                                        | 一   | 二   | 三   | 四   | 五   | 六   |
| 25                                                        | 26   | 27   | 28   | 29   | 30   | 1    |
| 2                                                         | 3    | 4    | 5    | 6    | 7    | 8    |
| 9                                                         | 10   | 11   | 12   | 13   | 14   | 15   |
| 16                                                        | 17   | 18   | 19   | 20   | 21   | 22   |
| 23                                                        | 24   | 25   | 26   | 27   | 28   | 29   |
| 30                                                        | 31   | 1    | 2    | 3    | 4    | 5    |

### 搜索

 

 

### 常用链接

- [我的随笔](https://www.cnblogs.com/zfcblog/p/)
- [我的评论](https://www.cnblogs.com/zfcblog/MyComments.html)
- [我的参与](https://www.cnblogs.com/zfcblog/OtherPosts.html)
- [最新评论](https://www.cnblogs.com/zfcblog/RecentComments.html)
- [我的标签](https://www.cnblogs.com/zfcblog/tag/)

### 我的标签

- [odoo13学习之路(1)](https://www.cnblogs.com/zfcblog/tag/odoo13学习之路/)

### 随笔档案

- [2020年8月(4)](https://www.cnblogs.com/zfcblog/archive/2020/08.html)
- [2020年7月(3)](https://www.cnblogs.com/zfcblog/archive/2020/07.html)
- [2020年6月(2)](https://www.cnblogs.com/zfcblog/archive/2020/06.html)
- [2020年3月(2)](https://www.cnblogs.com/zfcblog/archive/2020/03.html)

### 阅读排行榜

- [1. Linux之CentOS 7镜像下载（附带安装教程）(2107)](https://www.cnblogs.com/zfcblog/p/13582659.html)
- [2. Linux中提示没有pip命令解决办法(1893)](https://www.cnblogs.com/zfcblog/p/13583704.html)
- [3. nginx 中location和root，你确定真的明白他们关系？(335)](https://www.cnblogs.com/zfcblog/p/13361634.html)
- [4. Django项目中把原生sqlite数据迁移至mysql数据库(296)](https://www.cnblogs.com/zfcblog/p/13574066.html)
- [5. CentOS7安装python3.7.2，以及编译过程中出现的问题(260)](https://www.cnblogs.com/zfcblog/p/13585181.html)

### 推荐排行榜

- [1. Linux之CentOS 7镜像下载（附带安装教程）(1)](https://www.cnblogs.com/zfcblog/p/13582659.html)
- [2. 一些python牛人地址分享(1)](https://www.cnblogs.com/zfcblog/p/13360493.html)