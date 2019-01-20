# mydan supervisor
```
root@feng-pc:~# mydan supervisor
SYNOPSIS
     $0 --cmd ./myserver --log /tmp/mylog/path [--size 10000000 ] [--keep 5] [--name myprocname]
     $0 --cmd ./myserver --log /tmp/mylog/path --http http://127.0.0.1:8080
     $0 --cmd ./myserver --log /tmp/mylog/path --http http://127.0.0.1:8080 --check OK
         --count 10
```
> * 守护的方式启动进程

## 参数

> * cmd 要守护的命令 
> * log 日志目录
> * size 一个日志文件的大小
> * keep 保留几个日志文件
> * name 守护进程名称
> * count 被守护的进程的启动次数，超过这个次数就不在守护，守护进程退出

> * http 检查http，如果检查结果不符合预期，重启cmd命令

## 例
```
root@feng-pc:/opt/mydan/dan/tools# mydan supervisor --cmd ./foo.pl --log /tmp/log/foo
root@feng-pc:/opt/mydan/dan/tools# tail /tmp/log/foo/current
@400000005c21c83400000000 [START:1]
@400000005c21c83400000000 [STDOUT] 1545717802
@400000005c21c83500000000 [STDOUT] 1545717803
@400000005c21c83600000000 [STDOUT] 1545717804
@400000005c21c83700000000 [STDOUT] 1545717805
@400000005c21c83800000000 [STDOUT] 1545717806


root@feng-pc:~# tail /tmp/log/foo/current |mydan tai64nlocal
2018-12-23 14:04:51.000000000 [STDOUT] 1545717891
2018-12-23 14:04:52.000000000 [STDOUT] 1545717892
2018-12-23 14:04:53.000000000 [STDOUT] 1545717893
2018-12-23 14:04:54.000000000 [STDOUT] 1545717894
2018-12-23 14:04:55.000000000 [STDOUT] 1545717895
2018-12-23 14:04:56.000000000 [STDOUT] 1545717896
2018-12-23 14:04:57.000000000 [STDOUT] 1545717897
```