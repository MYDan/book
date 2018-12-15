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

## 例
```
feng@feng-pc:~$ mydan shell -h 127.0.0.1
root@feng-pc:/home/feng#
```