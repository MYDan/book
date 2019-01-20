# 核心工具
## rcall

远程调用，在之前的例子展示过,

```
[root@feng-pc ~]#mydan rcall
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
> * 批量操作工具， 其中exec是执行命令的插件，[查看更多插件](/tools/rcall.md)

### 例
```
[root@feng-pc ~]#mydan rcall -r '127.0.0.1' exec w
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
 18:22:17 up 1 day,  2:45,  2 users,  load average: 0.30, 0.28, 0.34
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
feng     tty7     :0               11:34   18:44m 10.87s  2.75s /sbin/upstart --user
feng     pts/2    127.0.0.1        18:16    9.00s  0.52s  0.40s /opt/mydan/perl/bin/perl /opt/mydan/dan/tools/rcall -r 127.0.0.1 exec w
====================================================================
```

## grsync
```
[root@feng-pc ~]#mydan grsync
SYNOPSIS
     $0 [--src src-range(default `hostname`)] --dst dst-range --sp src-path [--dp dst-path] \
        [--timeout seconds(default 300)]
        [--max number(default 128)]
        [--retry number(default 2)]
        [--gave number(default 3)]
        [--user username(default `id -un`)]
        [--sudo user1 ]
        [--chown root]
        [--chmod 777]
        [--cc]
         -1      Forces grsync to try protocol version 1
         -2      Forces grsync to try protocol version 2
         -3      Forces grsync to try protocol version 3
         -4      Forces grsync to try protocol version 4
         --sp /path/file --dp /path/foo/newfile
         --sp /path/file --dp /path/foo/
         --sp /path/     --dp /path/foo/
         --sp /path/foo* --dp /path/foo/
         --sp '/path/file1;/path/file2' --dp /path/foo/
```
> * 批量同步文件的工具， [点击查看详情](/tools/grsync.md)

```
feng@feng-pc:~$ mydan grsync --src '127.0.0.1' --dst '127.0.0.1' --sp /tmp/file1 --dp /tmp/file2
------------------------------------------------------------
sp:/tmp/file1 => dp:/tmp/file2
127.0.0.1 => 127.0.0.1: RSYNC
127.0.0.1 <= 127.0.0.1: OK
============================================================
```

## shell
```
mydan shell -h 127.0.0.1
```
```
feng@feng-pc:~$ mydan shell -h 127.0.0.1
root@feng-pc:/home/feng#
```

> * 获取远程shell是通过反弹shell的方式，如果隔离网络环境，这个功能需要控制机需要有公网ip
> * mydan 2.0.0版本以上可以使用shellv2工具，这个不需要中控机有公网ip这个条件