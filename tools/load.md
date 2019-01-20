# mydan load
```
root@feng-pc:~# mydan load
SYNOPSIS
     $0 -host host [--sp srcfile] [--verbose]
         [--dp dstfile (default sp )]
         [--sudo sudoer ]
         [--user username (default `id -un`)]
         [--timeout seconds (default 500)]
         [--continue]
         [--chown root]
         [--chmod 777]
         [--cc]
```
> * 从远程机器下载文件

## 参数

> * host 指定下载的机器
> * sp 指定源路径地址
> * verbose 显示现在百分比
> * dp 指定下载到本地的路径，如果不指定，和sp路径一致
> * sudo 指定执行这个操作的用户
> * user 执行用户名，显示在远程机器的日志中
> * timeout 超时，单位秒
> * continue 续传
> * chown 目标文件的属主
> * chmod 目标文件的权限
> * cc 继承远程文件的属主和文件权限，如果指定chown或chmod，以指定的为准

## 例
```
root@feng-pc:# mydan load -h 127.0.0.1 --sp /opt/mydan/dan/tools/range --dp /tmp/range
position: 0
Load .. 100% 1352/1345
Load .. 100% 2697/1345
```
