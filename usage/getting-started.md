# 快速入门

服务都准备好了，应该如果使用，以下给大家逐步介绍一下

## 查看mydan

> * mydan安装完后，会在/bin/建一个软连接指向mydan的命令行工具，但也有特殊的情况(如在mac中)。
> * 如果没有/bin/mydan,可以直接执行/opt/mydan/bin/mydan

```
root@feng-pc:/tmp# mydan
Usage: mydan COMMAND [arg...]
Options:
        --dan   Switch to `dan` first.
        --box   Switch to `box` first.
        Help    show detail
Commands:
        * go    登陆服务器.
        * range 操作对象描述.
        * whois 查询、模糊查询机器信息.
        * gateway       代理.
        * rcall 远程调用mydan的agent.
        * rtail tail多个远程机器日志.
        * vssh  虚拟登陆多个机器.
        * mssh  批量ssh命令.
        * mcmd  批量命令.
        * load  从远程机器下载文件.
        * rsync 同步文件.
        * mrsync        批量同步文件.
        * grsync        全局批量同步文件，可以在多个隔离的网络中通过代理同步.
        * access        给远程机器添加用户.
        * keys  给运程机器添加key信任.
        * config        mydan配置.
        * shell 获取远程机器反弹shell.
        * alias mydan内部使用的alias.
        * unalias       mydan内部使用的unalias.
        * sync  同步mydan的配置
        * xtar  脚本和数据压缩工具.
        * git   git命令，添加了指定key功能.
        * alarm 设置超时闹钟运行命令.
        * bigest        查找大文件.
        * expect        自动应答.
        * release       发布mydan.
        * supervisor    守护方式启动进程.
        * tai64nlocal   查看tai64格式日志.
        * diagnosis     系统诊断.
        * tcpserver     脚本提供tcp服务.
        * deploy        本地发布切连接小工具.
        * secure        私密文件管理小工具.
        * diskSpaceControl      控制磁盘使用空间在某个百分比.
        * node  机器管理.
        * reborn        重装系统.
Run 'mydan COMMAND --help' for more information on a command.
```

## 尝试调用mydan远程命令
```
mydan rcall -r 127.0.0.1 exec w
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
 13:18:37 up 221 days, 20:38,  1 user,  load average: 0.08, 0.03, 0.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
root     pts/1    10.10.10.10    12:21    5.00s  0.94s  0.73s /opt/mydan/perl/bin/perl /opt/mydan/dan/tools/rcall -r 127.0.0.1 exec w
====================================================================
```

> * 如果这个可以调用的通，说明agent部署和启动正常。
> * 这里先不考虑隔离区域的情况，隔离区域在后续章节讨论