# mydan xtar
```
root@feng-pc:~# mydan xtar
SYNOPSIS
     $0 [--script script.sh] [--package foo.tar.gz] [--output file]
     package filename is $TMP in the script
```
> * 脚本和数据压缩工具，可以把命令和数据打包在一起

## 准备

### 压缩文件
```
root@feng-pc:/tmp/xx# mkdir -p foo && date > foo/time && tar -zcvf foo.tar.gz foo
foo/
foo/time
```
### 脚本
```
root@feng-pc:/tmp/xx# cat > foo.sh <<EOF
> #!/bin/bash
> tar -zxvf $TMP -C /tmp/ || exit 1
> cat /tmp/foo/time
> EOF
```

## 打包
```
root@feng-pc:/tmp/xx# mydan xtar  --script foo.sh  --package foo.tar.gz --output foo.123.sh
记录了0+1 的读入
记录了0+1 的写出
64 bytes copied, 0.000149426 s, 428 kB/s
记录了0+1 的读入
记录了0+1 的写出
206 bytes copied, 0.0145471 s, 14.2 kB/s
```

## 执行
```
root@feng-pc:/tmp/xx# ./foo.123.sh
记录了1+0 的读入
记录了1+0 的写出
1024 bytes (1.0 kB, 1.0 KiB) copied, 0.000157302 s, 6.5 MB/s
记录了0+1 的读入
记录了0+1 的写出
206 bytes copied, 0.000143735 s, 1.4 MB/s
foo/
foo/time
2018年 12月 23日 星期日 10:39:33 CST
```