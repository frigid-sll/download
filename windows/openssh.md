1，下载OpenSSH

下载地址：https://github.com/PowerShell/Win32-OpenSSH/releases

选择适合你电脑的zip，我下载的是OpenSSH-Win64.zip



2，在你的电脑上解压



3，按住shift，同时鼠标右键，打开cmd，执行：

powershell.exe -ExecutionPolicy Bypass -File install-sshd.ps1
4，防火墙入站出站规则，添加22端口。

高级安全windows防火墙->新建规则->特点端口->22，具体步骤省略



5，开启服务，下图圈住的2个，如果没有就在D:\OpenSSH-Win64文件夹里的exe文件用鼠标点一遍，如sftp-server.exe



6，Xshell连接输入用户名和密码就可以了

————————————————
版权声明：本文为CSDN博主「qq_41397201」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_41397201/article/details/83996448