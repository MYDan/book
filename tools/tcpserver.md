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

## 例
```
root@feng-pc:~# mydan tcpserver -p 65111 -m 10 /opt/mydan/dan/agent/bin/agent
```

> * mydan 的agent就是根据这个服务启起来的