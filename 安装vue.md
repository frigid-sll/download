#### 安装vue

**一、安装vue**

1、安装node.js，安装完node.js之后，npm也会自动安装

查询是否安装成功的命令：

node -v

npm -v

![img](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=817140848,2332321320&fm=173&app=49&f=JPEG?w=364&h=87&s=7A25A144E3F8A06808CB55860200A089)

2、全局安装脚手架工具vue-cli，命令如下：

npm下载速度慢，我们将它升级：

```
npm install -g cnpm --registry=https://registry.npm.taobao.org

cnpm install --global vue-cli
```



![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=257879488,2103907607&fm=173&app=49&f=JPEG?w=640&h=91)

3、vue项目初始化命令如下，若没有安装webpack，则先安装webpack

```
cnpm install -g webpack

vue init webpack myproject
```

注：安装过程 中有个选项（Use ESLint to line your code ?选择 No ）

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=206217202,4094068924&fm=173&app=49&f=JPEG?w=640&h=248&s=F2A5F148BBE09F701273CC850200F08B)

初始化完成后的vue项目目录如下：

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=4214703202,620057814&fm=173&app=49&f=JPEG?w=368&h=434&s=E1F2036752B4B66C0CD1D40F0000E0C3)

4、进入到myVue目录下，使用npm install 安装package.json包中的依赖

命令如下：

cd myVue

npm install

![img](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=1287911943,2770218222&fm=173&app=49&f=JPEG?w=640&h=96)

5、运行项目：

npm run dev

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=1556517163,2275415285&fm=173&app=49&f=JPEG?w=433&h=28)

![img](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=3584563017,4278090784&fm=173&app=49&f=JPEG?w=627&h=115&s=BA07F14CCFA4BF700CF6C59B0200F08B)

在浏览器上输入：localhost:8080，将会出现下面的vue初始页面：

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=921530914,603745497&fm=173&app=49&f=JPEG?w=640&h=586&s=49803C726B5A66CC587DC15D020050E2)

6、结束项目运行：

ctrl+v，选择Y即可停止项目的运行



#### **vue项目目录说明**



![img](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=3218365640,2384742699&fm=173&app=49&f=JPEG?w=369&h=643&s=E8F2A3435AE4B76C567454050000F0C3)

build：项目构建(webpack)相关代码

config：配置目录，包括端口号等

node_modules：npm加载的项目依赖块

src：这里是我们要开发的目录，基本上要做的事情都在这个目录里。里面包含了几个目录及文件：

assets: 放置一些图片，如logo等

**components：该目录里存放的我们的开发文件组件，主要的开发文件都存放在这里了**

**App.vue：项目入口文件**

**main.js：项目的核心文件**

**router：路由配置目录**

static：放置一些静态资源文件

test：初始测试目录，可删除

.xxxx文件：这些是一些配置文件，包括语法配置，git配置等

**index.html：首页入口文件**

package.json：项目配置文件

README.md：项目的说明文档，markdown 格式

**三、vue项目启动流程**

1、在执行npm run dev的时候，会去在当前文件夹下的项目中找package.json文件,启动开发服务器，默认端口是8080；



![img](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=1993508972,4047401773&fm=173&app=49&f=JPEG?w=640&h=253&s=20C09142DBE0B1705655DC0D0000F0C1)

2、找到src的main.js文件，在该文件中new Vue的实例，要加载的模板内容App；

![img](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=3013279965,1633850418&fm=173&app=49&f=JPEG?w=452&h=322&s=6041B34053F4B66B1CCD4C010000E0C0)

3、App是src目录下的App.vue结尾的文件；

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=927348574,2202134744&fm=173&app=49&f=JPEG?w=640&h=553&s=21C0B1409AA6B76C4E41540E0000E0C0)

4、在App.vue所对应的模板当中，有一个router-view在src目录下有一个router文件夹，该文件夹有个index.js文件，该文件是配置路由词典，指定了路由地址是空，加载HelloWorld组件



![img](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=911083013,1434273632&fm=173&app=49&f=JPEG?w=509&h=379&s=6061B34253E4B36C5C5D040F0000E0C0)

注：vue运行是基于node环境的,构建vue框架之前,需要确保node环境安装成功

**四、Vue的组件的使用**

1、在components文件夹下创建.vue结尾的文件

例如在：src/components/public/目录下新建header.vue文件

![img](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=3514243451,3794796354&fm=173&app=49&f=JPEG?w=363&h=143&s=FAE281441BE1BF6410E7DD0B0200A0CB)

header.vue文件内容如下：

![img](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=961392477,1719901887&fm=173&app=49&f=JPEG?w=640&h=291&s=29C0B34E1BE093640EDDF5060000E0C0)

2、在路由配置文件src/router/index.js中引入组件并配置组件路由

2.1、引入组件

import Header from '@/components/public/header'

2.2、配置组件路由

{

path: '/header',

name: 'header',

component: Header

}

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=4099868317,2212358334&fm=173&app=49&f=JPEG?w=536&h=537&s=E060B34253B6B26F56ED9C0F000070C0)

3、运行项目：npm run dev

4、在浏览器中输入：localhost:8080/header ,显示如下页面：

![img](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=2013344042,2621465106&fm=173&app=49&f=JPEG?w=465&h=299&s=49803C7279E077053777475D0200C0E2)

**附：vue生命周期示意图**

![img](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=3865911803,2670798241&fm=173&app=49&f=JPEG?w=640&h=1621&s=5DA03C729FEA44015CC4D04E020060F3)