# mydan rtail
```
root@feng-pc:~# mydan rtail
SYNOPSIS
     $0 --range range /file/1 /file/2
     $0 --range range #default filelist in remote /etc/mydan.file
        tail file from remote machine
     $0 --range range --listen 9999
     $0 --range range --listen 9999 [--addr 10.10.10.1]\
          [--user user(default `id -un`)] [--sudo sudoer]
       --seek T0 (defaule) || --seek H0 || --seek T1024
```

> * 获取远程机器的实时日志.mydan中的mydan rcall可以批量调用命令，但是这个必须等命令执行结束才能返回，所以使用不了tail -f foo这种类型的远程调用，mydan中的mydan shell可以获取远程机器的shell，可以交互式的操作机器，当然也可以执行tail -f foo，但是这个命令一次只能针对一台机器，所以如果你需要实时的获取多个机器的远程日志，这个时候就需要用到mydan rtail

## 参数
> * range 操作对象
> * listen 监听端口，如果不指定，会在65112-65535端口中找一个没在使用的端口
> * addr 远程机器日志输出到的tcp的ip地址

## 例

## 原理
> * mydan rtail会其中的时候会启动一个随机的端口
> * 通过mydan rcall功能去远程打开文件，并把输出流直到中控机中rtail开启的端口， mydan rcall退出
> * 中控机器获取和显示远程日志，如果中控机的rtail命令退出后，远程的采集日志的进程也一并退出
