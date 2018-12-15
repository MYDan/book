# 监控管理

## 路径
> * /opt/mydan/dan/monitorv2

## 编辑配置
```
root@feng-pc:/opt/mydan/dan/monitorv2/conf# cat sysinfo
---
target: localhost,127.0.0.1
interval: 60
code: sysinfo
param:
  test:
    cpu:
      - '{CPU}{all}{%idle} < 10'
      - '{CPU}{all}{%idle} > 1'
      - '{CPU}{all}{%user} > 90'
    disk:
      - '{DF}{/da10}{Use%} > 90'
      - '{DF}{/da11}{Use%} > 90'
      - '{DF}{/da12}{Use%} > 90'
      - '{DF}{/da14}{Use%} > 90'
      - '{DF}{/da1}{Use%} > 90'
```

> * 每一个监控对应一个配置文件,默认情况下有grep,http,sysinfo, test的配置

> * target: range表达式，描述监控的对象
> * interval: 监控的频率
> * code: 监控的插件
> * param: 监控插件的参数


# 管理

## 查看任务
```
root@feng-pc:/opt/mydan/dan/monitorv2/bin# ./control
grep: started.
http: stoped.
sysinfo: started.
test: stoped.
```
> * 这里会显示监控的任务的状态，是启动的还是停止的

## 启动任务
```
root@feng-pc:/opt/mydan/dan/monitorv2/bin# ./control --start sysinfo
```

## 查看日志
```
root@feng-pc:/opt/mydan/dan/monitorv2/bin# ./control --tail sysinfo
                      'lijinfeng2011@gmail.com'
                    ]
        };
email:private
$VAR1 = {
          'user' => [
                      'lijinfeng2011@gmail.com'
                    ],
          'mesg' => {
                      'time' => '2018-12-15_16:31:23',
                      'name' => 'null',
                      'attr' => 'null',
                      'mesg' => 'name:null attr:null scale:(1/1) strategy: {CPU}{all}{%idle} > 1 node:localhost'
                    },
          't' => 'email'
        };
analysis: done.
batch: begin.
batch: done.
collector: begin.
collector: done.
analysis: begin.
```

## 停止任务
```
root@feng-pc:/opt/mydan/dan/monitorv2/bin# ./control --stop sysinfo
```
