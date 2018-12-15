# 机器管理

```
[root@feng-pc tmp]# mydan node
Usage: mydan.node COMMAND [arg...]
Options:
        --dan   Switch to `dan` first.
        --box   Switch to `box` first.
        Help    show detail
Commands:
        * show  show出cache中的机器
        * dump  dump出data中的机器
        * cache 生成cache
        * load  load数据到数据库
          motify        修改数据
        * purge 删除数据
Run 'mydan.node COMMAND --help' for more information on a command.
```

## 编辑机器配置文件
* 编辑自己的机器管理的配置文件,文件中的结构分成四层
* 第一层是项目名或者cluster名，第二层为机器属性（比如机房信息，模块）， 第三层为操作对象（比如机器),第四层为资源状态（比如监控系统和发布系统中，状态为0的不处理）。

```
cat > hostdb <<EOF
---
project1:
  idc1:
    'localhost': 1
  idc2:
    '127.0.0.1': 1
EOF
```

## 加载配置文件

```
mydan node load hostdb
```

## dump出机器信息
```
mydan node dump  #dump出所有的机器信息
mydan node dump project1 #dump出项目名为project1的机器信息
mydan node dump project1 --compress #压缩显示
mydan node dump --output /tmp/hostdb #dump到指定文件中
```

## 生成缓存cache
```
mydan node cache
```
## 查看缓存
```
mydan node show 
mydan node show project1
```
> * 与dump类似，区别在于show是在cache中读取的数据

## 修改状态
```
mydan node modfiy  --range 127.0.0.1 -v 3 -c project1 -t idc1  # 把 project1下的idc1中的127.0.0.1状态改成3

mydan node cache #加载到缓存中
```

## 删除
```
mydan node purge --cluster project1 --table idc1 #删除project1下的所有idc1
```

## 其他

> * 机器管理中的cache在路径 /opt/mydan/etc/node/cache 下，如果出现问题，可以在这里进行回滚
> * 没有进入缓存之前的文件放在 /opt/mydan/etc/node/data 路径下


# 操作对象描述

有了机器管理，下面介绍一下操作对象描述

从机器管理中获取操作对象

#### 获取所有的机器
```
mydan node range '{==*==*??==*}'
```
#### 获取编号为1的所有机器:
```
mydan node range '{==*==*??==1}'

```

#### 通过插件的方式获取机器
/opt/mydan/dan/node/callback 下放了node的插件
默认情况下有两个插件，如果需要扩展可以自己开发

插件list， 在文件中获取机器列表：
如在目录/path/foo中有文件  a.list 和 b.list
cd 进入/path/foo目录运行
```
mydan range '{%%list==a}' #获取a.list 的机器列表
mydan range '{%%list==a,b}' #获取a.list 和b.list的机器列表
mydan range '{%%list}' #获取所有以 .list文件为后缀的机器列表
```

node插件
```
mydan range '{%%node}' #获取机器管理中全部机器
```

#### 表达式

```
mydan range 'node{1~100}' #获取 node1 到node100的列表
mydan range '{==project1==*??==*},10.10.10.10,-127.0.0.1,&/abc/' #获取project1下的所有机器，在加上10.10.10.10这个机器，在去掉127.0.0.1这个机器，在过滤出包涵字符abc的列表
```


# 操作

#### 这样就可以批量操作多个机器了

```
[root@feng-pc ~]# mydan rcall -r '{==*==*??==*}' exec w
run .. 100% 2/2
############################## RESULT ##############################
====================================================================
127.0.0.1,localhost[2]:
 16:00:30 up 221 days, 23:20,  2 users,  load average: 0.00, 0.01, 0.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
root     pts/1    10.10.10.10    12:21    3:02   2.06s  2.06s -bash
root     pts/2    10.10.10.10    14:58    6.00s  0.79s  0.71s /opt/mydan/perl/bin/perl /opt/mydan/dan/tools/rcall -r {==*==*??==*} exec w
====================================================================
```
