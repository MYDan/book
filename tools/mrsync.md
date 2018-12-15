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
