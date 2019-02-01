# mydan fastmd5
```
[root@feng-pc]# mydan fastmd5
SYNOPSIS
     $0 /path/file

```
> * 计算文件md5,如果文件大小大于2兆并且大于阈值（默认5G）,则直接计算文件的前1兆和最后1兆的内容加上文件的大小用来计算md5。（ $size:$head:$tail ）
> * 数据同步的时候使用fastmd5来计算文件的md5

## 例
```
[root@feng-pc]# time mydan fastmd5 /tmp/1G
4807b06b94db1cd9426d43c9d02ec2b6  /tmp/1G
real    0m0.197s
user    0m0.176s
sys     0m0.021s
```

## 阈值

### 查看阈值
```
[root@feng-pc]# mydan config util.fastmd5
5368709120
```

### 调整阈值
```
[root@feng-pc]# mydan config util.fastmd5=5368709121
[root@feng-pc]# mydan config util.fastmd5
5368709121
```

* > 在做文件同步的机器之间阈值要统一，否则会因为md5计算出来的结果不一致而出现同步失败的现象
