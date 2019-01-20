# mydan release
```
root@feng-pc:~# mydan release -?
Usage:
     $0
         show pack list
     $0 --pack v1.0
         package
     $0 --release v1.0
         release
```
> * 发布mydan, 把本地的mydan打包成一个可以运行的文件，方便拷贝到别的地方安装
> * 正常情况下用快速安装的方法安装就即可，但是有些不能上公网的情况下就需要把本地的mydan打包成一个可以执行的安装包
> * 如果是在dashboard的机器上打的包，在dasoboard页面上可以看到新打的包的版本，可以通过dashboard上的链接直接安装，否则在

## 例
```
root@feng-pc:/opt/mydan# mydan release --release v1.0

root@feng-pc:/opt/mydan# find /opt/mydan/  -name *v1.0*
/opt/mydan/etc/dashboard/download/agent/Linux.x86_64/mydan.v1.0.tar.gz
/opt/mydan/etc/dashboard/download/agent/Linux.x86_64/mydan.v1.0.client
/opt/mydan/etc/dashboard/download/agent/Linux.x86_64/mydan.v1.0.agent
/opt/mydan/tmp/release/v1.0
```

> * 工具会根据系统类型打包，例子中是Linux的x86_64的机器，把mydan.v1.0.agent 拷贝到要安装的机器上，允许这个脚本即可（这个脚本中已经包涵了数据和脚本是用mydan xtar压缩在了一起）