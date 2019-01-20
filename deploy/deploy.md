# 发布管理

## 路径
> * 工具路径： /opt/mydan/dan/deploy/bin
> * 发布流程路径：/opt/mydan/etc/deploy/conf
> * 发布过程配置：/opt/mydan/etc/deploy/mould

一个conf下的配置对应一个发布流程。发布流程可以共用mould下的发布过程配置。


## 编辑发布过程配置
```
root@feng-pc:～# cat /opt/mydan/etc/deploy/mould/apps.test
---
#-
#  title: show version
#  global: 1
#  check:
##  redo: 2
##  retry: 20
#  repeat: 1
#  delay: 2
##  sleep: 20
#  code: m.sync
#  goon: 25%
##  fix: 30
#  param:
#    bin: 'echo a b c d version: 011.1'
#    sp: /tmp/adas/a/sda/
#    user: search
#    proxy: foo
#    cont: '(version:.+)'
-
  title: Run a command
  code: m.exec
  goon: 25%
  param:
    bin: 'echo abc'
-
  title: ctrl apps
  code: m.apps
  goon: 25%
  param:
    name: project1
    ctrl: [ 'start' ]
-
  title: deploy
  code: m.deploy
  goon: 25%
  param:
    name: project1
    ctrl: [ 'deploy' ]
-
  title: mcmd
  code: m.mcmd
  goon: 25%
  param:
    bin: 'echo {}abc'
-
  title: check
  code: m.check
  goon: 25%
  param:
    check: [ 'project1' ]
```

> * 发布过程是一个数组，表示发布某一组机器的一系列动作。
> * title: 标题
> * code: 对应code目录中的插件
> * goon: 达到这个百分比才回继续往下走，否则会stuck，需要用ctrl去控制
> * param： 就是插件需要的参数

### 统一参数
> * title 步骤的标题
> * global 是否是全局
> * redo 重做次数
> * retry 重试次数，重试完后还是不正常就stuck
> * repeat 执行部分失败的时候，是否在重试重做的时候把所有的都重复执行
> * delay 延时执行，sleep对应的秒数在执行
> * sleep 执行完后sleep
> * code 插件
> * goon 判断步骤是否可以继续的阈值，一个数字或者百分比（如 100%），默认是100%
> * fix 和重试类似，区别是在fix的时候，已经出现了stuck的信息
> * param 插件的参数



## 编辑流程
```
root@feng-pc:～# cat /opt/mydan/etc/deploy/conf/apps.test
---
batch:
  code: b.node
  param:
    batch:
      - 1
      - 1:2
    target:
#      - 'localhost{1~10}'
      - '127.0.0.1'
maint:
  mould: apps.test
  macro:
    version: 0001
    aa: 0001
    bb: $env{bb}
    aabbcc: $env{aabbcc}
macro:
  a: 1
  b: 1
  bb: 22
  aabbcc: 11221
```

> batch: 表示获取机器分组，
    > * code: 分组的插件
    > * param: 分组的参数

> maint: 选择发布步骤配置
    > * mould: 对应mould目录中的文件名
    > * macro: 传递给mould的宏
> macro: conf 中的宏


## 运行一次发布
```
root@feng-pc:/opt/mydan/dan/deploy/bin# ./deploy  apps.test
[1]: [127.0.0.1]
===========================================================================
title: Run a command | step: 1| node:1
===========================================================================
###########################################################################
do ...
---------------------------------------------------------------------------
time: 2018-12-14_14:16:17
node[1]: 127.0.0.1
==============================
---
127.0.0.1[1]: "abc\n"
==============================
succ[1]:127.0.0.1
===========================================================================
title: ctrl apps | step: 1| node:1
===========================================================================
###########################################################################
do ...
---------------------------------------------------------------------------
time: 2018-12-14_14:16:17
node[1]: 127.0.0.1
==============================
---
127.0.0.1[1]: |
  start [1]: [#!/bin/bash
  echo start
  ]
  start
==============================
succ[1]:127.0.0.1
===========================================================================
title: deploy | step: 1| node:1
===========================================================================
###########################################################################
do ...
---------------------------------------------------------------------------
time: 2018-12-14_14:16:17
node[1]: 127.0.0.1
==============================
---
127.0.0.1[1]: |
  [stage]: wget -c -t 10  -q -O '/data/package/project1/v0.2/pack.md5' 'http://127.0.0.1:5555/download/package/project1/v0.2.md5'
  ERROR: run stage ERROR
==============================
[error]: goon: 0.25 succ: 0 err:
```

> * 其中apps.test 名字是conf中的文件名
> * 可以在命令后添加宏参数，如 ./deploy apps.test "abc=123" 


## 查看stuck情况

```
root@feng-pc:/opt/mydan/dan/deploy/bin# ./watch
---------------------------------------------------------------------------
name: apps.test
---
stuck:
  deploy:
    '1': 'error:goon: 0.25 succ: 0 err:'
```
## 解锁

```
root@feng-pc:/opt/mydan/dan/deploy/bin# ./ctrl  -R apps.test
```
> * 解锁完后发布继续执行

# 插件

> * 插件用前缀来区分类型，"b."开头的为分批插件，"m.“开头的是发布过程使用的插件
> * 分组插件要返回一个二维的数组
> * 发布流程插件返回的是操作成功的列表hash

## b.node
```
batch:
  code: b.node
  param:
    batch:
      - 1
      - 1:2
    target:
      - 'localhost{1~10}'
      - '127.0.0.1'
```

> * 这是conf中的配置，param是插件的参数，b.node 需要两个参数 target和batch，target 是range表达式的range。batch是分批的方式,也是数组的方式，数组和target一一对应，如果batch比target短，由batch数组最后的元素补齐。对于每一个元素用“:”分隔着获取多少元素，可以是数组也可以是白分比（如10%），获取不全的用最后一个来补。如 1:5%:10 表示第一批是1台机器，第二批是5%的机器，第三批是10%的机器，如果海域哦机器，后面就都是10%一批

## m.apps
```
-
  title: ctrl apps
  code: m.apps
  goon: 25%
  param:
    name: project1
    ctrl: [ 'start' ]
```
```
[root@feng-pc]# cat /opt/mydan/etc/project/apps/project1/start
#!/bin/bash
echo start
```
> * 执行应用操作

## m.check
```
-
  title: check
  code: m.check
  goon: 25%
  param:
    check: [ 'project1' ]
```
```
[root@feng-pc]# cat /opt/mydan/etc/project/check/project1
-
  addr: http://127.0.0.1:5555
  check: 'mydan'
#  type: post # type: get  default
#  data: a=1&b=2
#  Host: abc.org
-
  port: 8080
#  type: tcp # type: udp  default
#  host: abc.foo.org # host: 127.0.0.1 default
```
> * 检查应用

## m.deploy
```
  title: deploy
  code: m.deploy
  goon: 25%
  param:
    name: project1
    ctrl: [ 'deploy' ]
```
```
[root@feng-pc]# cat /opt/mydan/etc/project/deploy/project1
link: /data/apps/project1
path: /data/package/project1
```
> * 发布应用

## m.exec
```
-
  title: Run a command
  code: m.exec
  goon: 25%
  param:
    bin: 'echo abc'
```
> * 调用agent的exec，即执行远程命令

## m.lock
```
-
  title: Lock
  code: m.lock
  goon: 25%
```
> * stuck，让运行步骤在该位置停止

## m.mcmd
```
-
  title: mcmd
  code: m.mcmd
  goon: 25%
  param:
    bin: 'echo {}abc'
```

> * 批量执行命令，和tools中的mcmd一样

## m.sync
```
-
  title: sync
  code: m.sync
  goon: 25%
  param:
    sp: /tmp/file1
    dp: /tmp/file2
    src: 'localhost'
```
> * 同步数据
> * src 默认为中控机本地
> * timeout 超时时间，默认是60，单位秒
> * max 并发数，默认500
> * user 执行用户，默认root
> * sudo 真实的执行用户
> * chown 目标文件属主
> * chmod 目标文件权限
> * cc 等于1时继承源文件属性
