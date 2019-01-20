# mydan config
```
root@feng-pc:~# mydan config -?
Usage:
     $0
     $0 foo.bar=123
     $0 foo.bar --del
     $0 [--raw]
```
> * 读取、修改 mydan的配置

## 例
```
root@feng-pc:# mydan config agent
---
argv: /opt/mydan/dan/agent/argv
auth: /opt/mydan/etc/agent/auth
conf: /opt/mydan/dan/agent/conf
lib: /opt/mydan/dan/agent/lib
path: /opt/mydan/dan/agent/path
port: 65111
proxy: /opt/mydan/etc/agent/proxy
role: agent
root@feng-pc:# mydan config agent.port=65123
root@feng-pc:# mydan config agent
---
argv: /opt/mydan/dan/agent/argv
auth: /opt/mydan/etc/agent/auth
conf: /opt/mydan/dan/agent/conf
lib: /opt/mydan/dan/agent/lib
path: /opt/mydan/dan/agent/path
port: '65123'
proxy: /opt/mydan/etc/agent/proxy
role: agent
```