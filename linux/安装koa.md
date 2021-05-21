#### 安装koa

提供一个国内镜像安装方法，速度非常快，在直接npm模块失败的时候非常好用，使用npm --registry=[http://registry.npmjs.org](https://link.jianshu.com/?t=http://registry.npmjs.org) install XXXXX –XX 命令安装，只需要在install后面加上要安装的中间件名称和相应的参数即可。 

```
cd node-v9.0.0

mkdir project

cd project

npm init

vi package-lock.json(加入"private": true,)
{
    ...
    "private": true,
    ...
}

npm --registry=http://registry.npmjs.org install koa
```

 

 

 

 

 

 

 