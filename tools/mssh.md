# mydan mssh
```
root@feng-pc:~# mydan mssh
SYNOPSIS
     $0 -r range [--sudo sudoer] [--noop][--verbose] cmd ..
        [--user user (default `id -un`)]
        [--timeout seconds (default 500)]
        [--max number (default 128)] \
```
> * 批量的ssh命令

## 参数

> * range 操作的机器
> * sudo 要sudo到哪个用户执行
> * noop 只是把要执行的命令显示出来，不去执行，调试用
> * verbose 显示详细,按照机器节点输出文本格式，方便文本处理
> * user 执行的用户,也就是ssh -l 命令指定的用户
> * timeout 超时时间，单位秒
> * 并发数

## 配置

### 路径
> * /opt/mydan/etc/util/conf/pass
> * 为了防止更新mydan的时候配置文件被覆盖，可以把配置文件放在 /opt/mydan/etc/util/conf/pass.private

### 内容
```
root@feng-pc:~# cat /opt/mydan/etc/util/conf/pass.private
#localhost{1~100}:
#  user1: "passwd1"
#  user2: "passwd2"
#node1:
#  uu: pp
#  default: ppp
#default:
#  u1: p1
#  default: p
#
10.10.10.144:
  root: KqwdblFQZD6TSVML
10.10.10.145:
  root: XnAYuEq4zCO8ULHi
```

> * default 表示缺省的，可以对所有机器配置上缺省密码，可以给部分机器设置缺省的密码

## 例子
```
root@feng-pc:/opt/mydan/dan/tools# mydan mssh   -r '10.10.10.{144,145}' 'hostname'
run .. 100% 2/2
############################## RESULT ##############################
====================================================================
10.10.10.144[1]:
10-10-10-144
====================================================================
10.10.10.145[1]:
10-10-10-145
====================================================================
root@feng-pc:/opt/mydan/dan/tools# mydan mssh --verbose  -r '10.10.10.{144,145}' 'hostname'
10.10.10.144:10-10-10-144
10.10.10.145:10-10-10-145
您在 /var/mail/root 中有新邮件
root@feng-pc:/opt/mydan/dan/tools# mydan mssh  -r '10.10.10.{144,145}' 'hostname' --noop
/usr/bin/ssh -o StrictHostKeyChecking=no -o NumberOfPasswordPrompts=1 -t -l root 10.10.10.144 hostname\;
/usr/bin/ssh -o StrictHostKeyChecking=no -o NumberOfPasswordPrompts=1 -t -l root 10.10.10.145 hostname\;
```
