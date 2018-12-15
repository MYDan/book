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

> * 获取远程机器的实时日志
 