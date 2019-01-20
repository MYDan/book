# mydan mrsync
```
root@feng-pc:~# mydan mrsync
SYNOPSIS
     $0 [--src src-range(default `hostname`)] --dst dst-range --sp src-path [--dp dst-path] \
        [--timeout seconds(default 300)]
        [--max number(default 128)]
        [--retry number(default 2)]
        [--gave number(default 3)]
        [--user username(default `id -un`)]
        [--sudo user1 ]
        [--chown root]
        [--chmod 777]
        [--cc]
         -1      Forces mrsync to try protocol version 1
         -2      Forces mrsync to try protocol version 2
```

> * ssh协议和mydan协议都支持mrsync工具，通过mydan --dan 和mydan --box 来切换协议
> * mrsync工具不支持多区域之间的同步，如果是要同步多个隔离的区域，请用 mydan grsync 工具
> * 如果使用的是ssh协议，要操作的机器之间需要ssh key，这些机器之间不需要密码，可以使用mydan keys命令来把ssh key下发到所有机器

## 协议

### dan
```
root@feng-pc:# mydan --dan
Switch to `dan` first.
root@feng-pc:# mydan mrsync
SYNOPSIS
     $0 [--src src-range(default `hostname`)] --dst dst-range --sp src-path [--dp dst-path] \
        [--timeout seconds(default 300)]
        [--max number(default 128)]
        [--retry number(default 2)]
        [--gave number(default 3)]
        [--user username(default `id -un`)]
        [--sudo user1 ]
        [--chown root]
        [--chmod 777]
        [--cc]
         -1      Forces mrsync to try protocol version 1
         -2      Forces mrsync to try protocol version 2

```
#### 参数
> * src 源机器，可以是多个机器，不指定时默认是本机
> * dst 目标机器，可以是多个
> * sp 源路径
> * dp 目标路径，如果不指定，和源路径一致
> * timeout 超时，单位秒
> * max 并发数
> * retry 重试次数，默认失败后重试两次
> * gave 一个源一次可以提供给多少个机器来拉取数据，默认是3个
> * user 这个用户只是用于打日志，真正的用户用sudo指定
> * sudo sudo的用户，真正执行的用户
> * chown 文件属主
> * chmod 文件权限
> * cc 继承源文件属主和文件权限，如果指定了chown或chmod，以指定的为准

### box
```
root@feng-pc:# mydan --box
Switch to `box` first.
您在 /var/mail/root 中有新邮件
root@feng-pc:# mydan mrsync
SYNOPSIS
     $0 [--src src-range(default `hostname`)] --dst dst-range --sp src-path [--dp dst-path] \
        [--timeout seconds(default 300)]
        [--max number(default 128)]
        [--retry number(default 2)]
        [--gave number(default 3)]
        [--nice number]
        [rsync options]

```
#### 参数
> * src 源机器，可以是多个机器，不指定时默认是本机
> * dst 目标机器，可以是多个
> * sp 源路径
> * dp 目标路径，如果不指定，和源路径一致
> * timeout 超时，单位秒
> * max 并发数
> * retry 重试次数，默认失败后重试两次
> * gave 一个源一次可以提供给多少个机器来拉取数据，默认是3个
> * nice nice级别
> * rsync options, rsync的其他参数
