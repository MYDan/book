# mydan access
```
root@feng-pc:~# mydan access
SYNOPSIS
     $0 -r range [--delete] [--add] users1 user2 ..
     Add or delete some users on the remote machine
     Only root users can execute
```
> * 给远程机器添加或者删除账号
> * 修改/etc/{passwd,shadow,group,sudoers}这四个文件,修改规则是qr/^$user\b/,添加用户时把控制机上的这四个文件匹配到的用户内容提取出来，写到远程机器上， 删除时在远程机器上找到匹配的内容进行删除
> * 添加用户时会创建家目录，删除用户时不删除家目录

## 例
```
[root@feng-pc]# mydan access  -r '10.10.10.{1,2}' --add user1
---
10.10.10.1: "ok\n--- 0\n"
10.10.10.2: "ok\n--- 0\n"
```

```
[root@feng-pc]# mydan access  -r '10.10.10.{1,2}' --delete user1
---
10.10.10.1: "ok\n--- 0\n"
10.10.10.2: "ok\n--- 0\n"
```

> * 删除的时候不会删除家目录
