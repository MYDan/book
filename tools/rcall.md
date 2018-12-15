# mydan rcall
```
root@feng-pc:~# mydan rcall
SYNOPSIS
     $0 -r range [--sudo sudoer ] [--verbose] cmd ..
         [--user username (default `id -un`)]
         [--timeout seconds (default 60)]
         [--max number ( default 128 )]
         [--port number ( default from .config )]
         [--env "A=123;B=abc" ]
         [--version]
         [--secret "x=1;xx=2" ]
```
> * 远程调用mydan中agent插件的命令

## 插件
```
root@feng-pc:~# ls /opt/mydan/dan/agent/code/
access  apps  call  check  collector  deploy  download  dump  edump  exec  filelist  grep  load  mrsync  proxy  reborn  scripts  sdump  sexec  shell  show  sysinfo  tail2tcp  version
```
> * access 添加用户权限的
> * apps 解析应用操作
> * call 调用命令
> * check 检查项目
> * collector 采集mydan collector收集到的数据
> * deploy 发布插件
> * download 下载文件的插件
> * dump 把文件dump到远程机器
> * edump 普通dump
> * sdump secret dump
> * exec 执行命令
> * sexec secret exec
> * filelist 获取文件列表，grsync插件会用到
> * grep 监控系统用的日志监控插件
> * load load文件
> * mrsync 代理上运行的mrsync插件
> * proxy 代理插件
> * reborn 远程重装系统
> * scripts 执行脚本，项目管理中的脚本
> * shell 远程shell
> * show 显示参数，用于调试
> * sysinfo 基础监控的插件
> * tail2tcp rtail工具使用的插件
> * version 获取mydan的版本

## 例
```
root@feng-pc:~# mydan rcall -r 127.0.0.1 exec w
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
 16:06:50 up 5 days, 29 min, 10 users,  load average: 0.35, 0.46, 0.43
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
feng     tty7     :0               二11    4days 40.01s 37.19s /sbin/upstart --user
====================================================================
```