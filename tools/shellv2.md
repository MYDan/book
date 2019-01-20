# mydan shell
```
root@feng-pc:# mydan shellv2
SYNOPSIS
     $0 --host host
        get a shell from remote machine
     $0 --host host [--user user(default `id -un`)] [--sudo sudoer]
```
> * 获取远程shell, 没有mydan shell相比，这个不需要控制机有外网ip，也不需要被控制机可以上公网

## 参数
> * host 要操作的机器
> * user 操作用户，只用于显示在远程服务器日志中
> * sudo 真正执行的用户，即获取的是这个用户的shell

## 原理
> * shellv2和shell一样都是反弹远程机器的bash，他们的区别是，shell是直接把反弹的tcp连接到控制机器上。shellv2则是把bash反弹到了agent上，中控机也连接到agent上，然后两个tcp对接起来

## 例
```
feng@feng-pc:~$ mydan shellv2 -h 127.0.0.1
root@feng-pc:/home/feng#
```

## 注
> * 这个需要mydan在2.0.0版本以上
