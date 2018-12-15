# mydan supervisor
```
root@feng-pc:~# mydan supervisor
SYNOPSIS
     $0 --cmd ./myserver --log /tmp/mylog/path [--size 10000000 ] [--keep 5] [--name myprocname]
     $0 --cmd ./myserver --log /tmp/mylog/path --http http://127.0.0.1:8080
     $0 --cmd ./myserver --log /tmp/mylog/path --http http://127.0.0.1:8080 --check OK
         --count 10
```
> * 守护的方式启动进程