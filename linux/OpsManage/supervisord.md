supervisor手动关闭：

\#/usr/bin/supervisorctl stop all先关闭supervisor启动脚本，之后再关闭supervisord服务



重新启动
supervisorctl reload
1
查看进程
supervisorctl status
1
启动某个进程
supervisorctl start xxxx
1
停止某个进程
supervisorctl stop xxxx
1
重启某个进程
supervisorctl restart xxxx