# mydan go
```
[root@feng-pc ~]# mydan go
SYNOPSIS
     $0 host [user]
     $0 --user dan host [user]
```
> * 这个命令用于快捷登录机器
> * mydan g 和 mydan go 两个命令等同

## 配置文件1
```
root@feng-pc:~# cat /opt/mydan/etc/util/conf/pass
#localhost{1~100}:
#  user1: "passwd1"
#  user2: "passwd2"
#node1:
#  uu: pp
#  default: ppp
#default:
#  u1: p1
#  default: p
```

> * 登录方式: mydan go foo ， 其中foo为机器名、ip，或者是node管理中的机器列表的部分内容
> * 用于登录node管理中的机器，或者指定机器名或者ip
> * 可以把配置文件改名成 /opt/mydan/etc/util/conf/pass.private避免更新mydan后被覆盖

## 配置文件2
```
root@feng-pc:~# cat   /opt/mydan/etc/util/conf/go
---
lijinfeng:mydan-slave:
  expect:
    assword: $ENV{PASSWD}
    code: googlecode:$ENV{TOKEN}
  go: ssh lijinfeng2011@gmail.com@op.mydan.org -t "ssh -t -i ~/key work@{} sudo su -
    root"
  range: mydan-slave-{1,2}
lijinfeng:mydan-test:
  expect:
    assword: $ENV{PASSWD}
    code: googlecode:$ENV{TOKEN}
  go: ssh lijinfeng2011@gmail.com@op.mydan.org -t "ssh -t -i ~/key work@{} sudo su -
    root"
  range: mydan-test-0{1,2}
```
> * 登录方式: mydan go /foo ， 其中foo是配置文件中的key
> * 可以把配置文件名改名成/opt/mydan/etc/util/conf/go.private，避免mydan更新后被覆盖
> * 配置文件中可以通过 $ENV{ABC}的方式在配置文件中使用变量
> * googlecode 为googlecode 验证