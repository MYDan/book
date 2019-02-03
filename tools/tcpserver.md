# mydan tcpserver
```
root@feng-pc:~# mydan tcpserver
SYNOPSIS
     $0 [--port num] [--max num] script
     [--whitelist file]
```
> * 把脚本提供成tcp服务

## 参数

> * port 端口
> * max 最大连接数
> * whitelist 白名单列表，可以不指定，不指定表示全部开放

## 限速

### 查看配置
```
root@feng-pc:# mydan config tcpserver
---
ReservedSpaceCount: 10
ReservedSpaceSize: 2
rbuf: 104857600
rlimit: 20971520
wlimit: 20971520
```
> * rlimit , 入流量的限制，单位B
> * wlimit , 出流量的限制，单位B
> * 限速默认都是20兆

### 修改配置
```
mydan config tcpserver.rlimit=20971520
```
> * 修改配置需要重启tcpserver服务

## 例
```
root@feng-pc:~# mydan tcpserver -p 65111 -m 10 /opt/mydan/dan/agent/bin/agent
```

> * mydan 的agent就是根据这个服务启起来的
