`windows`的`IIS`上发布部署项目(`vue前端`+`python后端`项目）

项目实现
`IIS`安装
既然部署到`IIS`上，那就必须要安装好`IIS。`
控制面板–>程序–>启用或关闭windows功能(将图中圈住的内容全部勾选)

项目组成

运行项目验证：

```
python manage.py runserver
```

验证没有问题进入下一步
安装`wfastcgi`模块

```
pip install wfastcgi
```



将安装好的`wfastcgi.py`文件拷贝到工程项目根目录下。

网站配置
打开`IIS`，新建网站。

添加程序映射
选中你发布的网站–>处理程序映射–>添加模块映射

```
请求路径：*
模块：FastCgiModule
请求限制要取消√
```



可执行文件是`python.exe`路径|`wfastcgi.py`路径
填写完参数后选择请求限制将对勾取消

进入`FastCGI`设置
点击主页

点击添加应用程序

添加环境变量–>增加两个键值对

```
Name: WSGI_HANDLER 
Value: django.core.wsgi.get_wsgi_application()
Name: DJANGO_SETTINGS_MODULE
Value:myproject.settings（myproject是自己的项目名称)
```



`应用程序池->你的网站->高级设置`

```
将标识中的ApplicationPoolidentity改为LocalSystem
```



到此，没有静态文件的项目才部署好。

修改`setting.py`文件中

```
ALLOWED_HOSTS = ['*']
STATIC_URL = '/static/'
STATICFILES_DIRS=[
    os.path.join(BASE_DIR,'dist/static'),
]
STATIC_ROOT =os.path.join(BASE_DIR, 'static')
```



2、配置静态文件
在项目中新建static文件夹，新建`web.config`文件。在其中添加以下代码


```
<?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
      <!-- this configuration overrides the FastCGI handler to let IIS serve the static files -->
      <handlers>
        <clear/>
	<!-- the configuration document write by Kahn.xiao -->
   <add name="StaticFile" path="*" verb="*" modules="StaticFileModule" resourceType="File" requireAccess="Read" />
     </handlers>
   </system.webServer>
</configuration>
```

3、收集静态文件

```
python manage.py collectstatic
```



身份验证-->匿名身份验证   添加你的用户即可

此时通过`IIS`访问网站即可了





