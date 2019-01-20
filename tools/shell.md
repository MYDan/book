# mydan shell
```
root@feng-pc:~# mydan shell
SYNOPSIS
     $0 --host host
        get a shell from remote machine
     $0 --host host --listen 9999
     $0 --host host --listen 9999 [--addr 10.10.10.1]\
          [--user user(default `id -un`)] [--sudo sudoer]
```
> * 获取远程shell

## 参数
> * host 要操作的机器
> * sudo 获取该用户的shell
> * user 执行人，只是显示在远程机器的日志中

> * listen 中控机监听端口，默认在65112 .. 65535中找一个没有被使用的端口
> * addr shell反弹的地址，默认情况下是被操作的机器获取到调用的ip地址，如果是多区域情况下，需要指定为中控机的外网ip，否则被控制机会跳转到代理机器的内网ip

## 安全
> * 反弹shell会先验证uuid才会把tcp连接建立起来

## 例
```
feng@feng-pc:~$ mydan shell -h 127.0.0.1
root@feng-pc:/home/feng#
```

## 注
> * 如果中控机没有外网ip，需要用mydan shellv2命令替代，这个需要安装2.0.0版本以上的mydan
