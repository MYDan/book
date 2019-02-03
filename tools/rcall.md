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

         [--immediately]
         [--addr 10.10.10.10]
         [--listen 9999]
```
> * 远程调用mydan中agent插件的命令

## 命令行参数

> * sudo 调用插件使用的用户，默认不sudo的情况下，用的是agent启动时的用户
> * verbose 如果指定这个参数，输出格式会变化成 node:output,方便文本处理
> * user 操作用户
> * timeout 默认60秒
> * max 并发数，默认128,如果操作使用了区域代理，并发数会变大，每个区域单独使用该并发数
> * port agent的端口，默认在配置文件中读取为65111
> * env 远程机器会先设置这临时些环境变量再执行对应的插件
> * version返回结构内包含远程机器mydan的版本
> * secret 传递秘密字段，远程机器日志中不显示该字段，sexec和chpasswd插件会用到

> * immediately 实时查看调用插件的输出内容，这个要看插件的实现是否有这个功能，目前scriptsx插件有这个功能
> * addr 如果使用了immediately参数，addr参数用来控制日志内容连接到的ip地址，默认是客户中获取到的远程机器的ip。如果存在代理的情况，请指定成控制机的外网ip
> * listen, 和addr参数类似，如果使用immediately参数的情况下指定的收取实时日志的端口。默认情况下在控制机上65112～65535的端口内找一个没在使用的

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

## 插件

> 路径 /opt/mydan/dan/agent/code/


### access
> * 添加删除用户,工具[mydan access](/tools/access.md)中有介绍

### apps 
> * 解析应用操作，在[应用操作](/deploy/project.md)中有过介绍

### call
```
[root@feng-pc]# mydan rcall -r 127.0.0.1 call 'echo abc' 'echo 123'
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
call[1]: [echo abc]
abc
call[2]: [echo 123]
123
====================================================================
```
> * 调用命令,可以调用多个命令. 多个命令在exec插件中也可以调用（如 mydan rcal -r host exec 'echo abc && echo 123'），call和exec有一些差别，call用的是system命令来调用，exec用的是exec命令调用，exec插件在调用过程中如果控制端ctrl+C停止掉，远程对应调用的命令如果没有执行完成，会被强制退出。call插件则不会.
如果exec插件调用的多个命令，也会导致ctrl+C的时候进程不退出，因为信号是发给父进程

### check
> * check 检查项目，在[应用操作](/deploy/project.md)中有过介绍

### chpasswd
```
[root@feng-pc]# mydan rcall --verbose  -r 127.0.0.1 chpasswd user1 user2 user3 --secret PASSWD=20AWjLFwBOHlra5M
run .. 100% 1/1
127.0.0.1:user1:20AWjLFwBOHlra5M
127.0.0.1:user2:20AWjLFwBOHlra5M
[root@feng-pc]# mydan rcall --verbose  -r 127.0.0.1 chpasswd user1 user2 user3
127.0.0.1:user1:J4Lx2MFVwUUW0se7
127.0.0.1:user2:PmV2ist69IfzXCmO
```

> * chpasswd 修改密码
> * 可以指定密码也可以不指定，不指定情况下随机生成
> * 使用--verbose 参数，当操作多机器多用户的时候，输出格式比较统一
> * 如果远程机器没有对应的用户，则跳过


### collector
> * collector 采集mydan collector收集到的数据

### deploy
> * deploy 发布插件，在[应用操作](/deploy/project.md)中有过介绍

### download
> * download 下载文件的插件

### dump
```
[root@feng-pc]# mydan rcall -r 127.0.0.1 dump file1  --path /tmp/file2 --chmod 777 --chown work
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
ok
====================================================================
[root@10-60-79-144 tools]# mydan rcall -r 127.0.0.1 exec 'ls -l /tmp/file2'
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
-rwxrwxrwx 1 work work 23 Dec 17 17:16 /tmp/file2
====================================================================
```
> * --path 目标文件绝对路径，如果不写则和源文件路径一致
> * 把文件dump到远程机器, --chmod 会改变文件权限(默认由远程机器agent启动时的umask决定)， --chown 改变文件归属(默认为远程机器启动的用户)
> * 可以添加参数 --cc 表示继承源文件的属性， 如果指定chmod或者chown 则属性由chmod和chown决定

### edump
> * edump 普通dump，不适合dump大文件,逻辑简单

### sdump
> * sdump secret dump，不适合dump大文件

### exec
```
[root@feng-pc]# mydan rcall -r 127.0.0.1 exec 'date && echo ok'
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
Mon Dec 16 17:14:54 CST 2018
ok
====================================================================
```
> * exec 执行命令

### sexec
```
[root@feng-pc]# mydan rcall -r 127.0.0.1 exec 'echo xxx__FOO'
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
xxx__FOO
====================================================================
[root@feng-pc]# mydan rcall -r 127.0.0.1 sexec 'echo xxx__FOO' --secret "FOO=123"
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
xxx123
====================================================================
```
> * sexec secret exec,功能和exec一样是执行命令，区别是它会替换 --secret 指定的变量，而且这个变量在远程机器上的日志是不显示的，如chpasswd插件也用了这个方式

### filelist
> * filelist 获取文件列表，grsync插件会用到

### grep
> * grep 监控系统用的日志监控插件

### load
> * load load文件

### mrsync
> * mrsync 代理上运行的mrsync插件，不手动调用

### proxy
> * proxy 代理插件，一般不手动调用

### reborn
> * reborn 远程重装系统

### scripts
```
[root@feng-pc]# cat start.sh
#!/bin/bash
echo start
[root@feng-pc]# mydan rcall -r 127.0.0.1 scripts start.sh
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
start
====================================================================
```
> * 调用控制机上的脚本，会把脚本的内容传到远程去执行

### scriptsx
> * 和scripts功能类似，不过多了实时查看脚本标准输出的功能

### shell
> * shell 远程shell,工具[mydan shell](/tools/shell.md)中有介绍

### show
```
[root@feng-pc]# ./rcall -r 127.0.0.1 show a b c
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
---
argv:
- a
- b
- c
code: show
sudo: ~
user: root
====================================================================
```
> * show 显示参数，用于调试,可以看出插件获取到的数据结构

### sysinfo
```
root@feng-pc# mydan rcall -r  127.0.0.1 sysinfo '{CPU}{all}{%idle} > 10'
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
---
temp###{CPU}{all}{%idle} > 10: '67.68'
====================================================================
root@feng-pc# mydan rcall -r  127.0.0.1 sysinfo '{CPU}{all}{%idle} < 10'
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
====================================================================
```
> * sysinfo 基础监控的插件,一般情况下不手动执行

### tail2tcp
> * tail2tcp rtail工具使用的插件,工具[mydan rtail](/tools/rtail.md)就是用的这个插件


### version
```
[root@feng-pc]# ./rcall -r 127.0.0.1 version
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
runtime version:001053
file version:001053
====================================================================
```
> * version 获取mydan的版本,runtime 表示agent启动的版本，file表示本地文件更新到的版本，如果两个版本不一样，说明更新mydan后agent没有重启 

### zipdir
> * grsync 用于压缩目录的插件

### unzipdir
> * grsync 用于解压目录的插件

### cleandir
> * grsync 用于清理临时文件的插件
