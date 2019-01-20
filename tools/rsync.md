# mydan rsync
```
root@feng-pc:~# mydan rsync
SYNOPSIS
     $0 -aP /tmp/foo user@host:/tmp/bar

```
> * 可以通过应答方式用ssh协议同步文件
> * 结合gateway可以方便把文件同步到任何地方

## 例
```
root@feng-pc:/opt/mydan/dan/tools# mydan rsync  -aP /tmp/foo root@10.10.10.144:/tmp/bar
root@10.10.10.144's password:
sending incremental file list
foo
             43 100%    0.00kB/s    0:00:00 (xfr#1, to-chk=0/1)
```

## 配置

> * 密码配置文件和mydan mssh中使用的配置文件一样
