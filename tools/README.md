# 工具详解

以下对下面命令做详细解释

```
[root@10-60-79-144 code]# mydan
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
        * shellv2 获取远程机器反弹shell的v2版本.
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
        * check 检查服务的小工具.
        * secure        私密文件管理小工具.
        * diskSpaceControl      控制磁盘使用空间在某个百分比.
        * node  机器管理.
        * reborn        重装系统.
Run 'mydan COMMAND --help' for more information on a command.
```

> * 可以通过mydan --dan 和 mydan --box进行切换
