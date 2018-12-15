# mydan gateway
```
root@feng-pc:～# mydan gateway -?
Usage:
     $0
     $0 on | off
     $0 on abc
     $0 off foo bar
     $0 restart | oo # oo and restart are the same, oo == off on
     $0 --help
```

## 配置
```
root@feng-pc:~# cat /opt/mydan/etc/util/conf/gateway
pek:
  go: 'ssh  -qTNf -D 127.0.0.1:12345 $ENV{MYUSERNAME}@gw1.mydan.org'
  expect:
    code: 'googlecode:$ENV{TOKEN_N}'
    assword: $ENV{PASSWD}
aws:
  go: 'ssh  -qTNf -D 127.0.0.1:12346 $ENV{MYUSERNAME}@gw2.mydan.org'
  expect:
    code: 'googlecode:$ENV{TOKEN_W}'
    assword: $ENV{PASSWD}
```
> * ssh代理，把跳板机，或者把其他区域的网络出口代理管理起来，方便mydan go工具做登录操作
> * mydan go 中的ssh命令可以配置成 ssh -o ProxyCommand='nc -x 127.0.0.1:1080 %h %p' username@server的方式来使用该代理
