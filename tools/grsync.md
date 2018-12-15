# mydan grsync
```
root@feng-pc:~# mydan grsync
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
         -1      Forces grsync to try protocol version 1
         -2      Forces grsync to try protocol version 2
         -3      Forces grsync to try protocol version 3
         -4      Forces grsync to try protocol version 4
         --sp /path/file --dp /path/foo/newfile
         --sp /path/file --dp /path/foo/
         --sp /path/     --dp /path/foo/
         --sp /path/foo* --dp /path/foo/
         --sp '/path/file1;/path/file2' --dp /path/foo/
```

> * 全局同步文件

#### 例
```
feng@feng-pc:~$ mydan grsync --src '127.0.0.1' --dst '127.0.0.1' --sp /tmp/file1 --dp /tmp/file2
------------------------------------------------------------
sp:/tmp/file1 => dp:/tmp/file2
127.0.0.1 => 127.0.0.1: RSYNC
127.0.0.1 <= 127.0.0.1: OK
============================================================
```