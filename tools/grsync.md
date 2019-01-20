# mydan grsync
```
root@feng-pc:~# mydan grsync
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

> * 全局同步文件

## 参数
> * src 源机器，默认是本机
> * dst 目标机器
> * sp 源路径
> * dp 目标路径，默认是sp
> * timeout 超时，单位秒
> * max 并发数，如果是同时操作多个区域，这个并发数在不同的版本中体现的不一样，一般情况下比你设置的要大
> * retry 失败后重试的次数，默认重试两次
> * gave 一个源同时可以给多少个机器提供数据
> * user 执行的用户，这个信息显示在远程机器的日志中，真正的执行用户用sudo指定
> * sudo 真正的执行用户
> * chown 文件属主
> * chmod 文件权限
> * cc 继承源文件的属性，如果指定了chown或chmod，以指定的为准

> * 协议版本，使用默认值即可

## sp和dp详解

> * --sp /path/file --dp /path/foo/newfile;源文件名是 /path/file,目标文件名为/path/foo/newfile
> * --sp /path/file --dp /path/foo/; 源文件名为/path/file; 目标文件名为/path/foo/file
> * --sp /path/     --dp /path/foo/; 把源目录下/path/下的文件同步到目标路径/path/foo/下
> * /path/foo* --dp /path/foo/; 把匹配/path/foo* 的文件同步到目标路径/path/foo/下
> * -sp '/path/file1;/path/file2' --dp /path/foo/; 把指定的文件用“;”分隔，把文件同步到目标路径下

## 例
```
feng@feng-pc:~$ mydan grsync --src '127.0.0.1' --dst '127.0.0.1' --sp /tmp/file1 --dp /tmp/file2
------------------------------------------------------------
sp:/tmp/file1 => dp:/tmp/file2
127.0.0.1 => 127.0.0.1: RSYNC
127.0.0.1 <= 127.0.0.1: OK
============================================================
```
