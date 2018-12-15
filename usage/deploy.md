# 发布系统

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
