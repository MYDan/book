# 订阅管理

> * 上一节中，我们已经把监控任务启动起来了，监控管理只负责去做检查相关的事情，报警发生后，这些信息发送给谁，这是由订阅系统来控制的。

## 路径
> * /opt/mydan/dan/subscribe/bin

## 查看当前订阅
```
root@feng-pc:/opt/mydan/dan/subscribe/bin# ./subscribe
name1|attr1|user1|1
name1|attr1|user1|1
name1|*|user1|1
*|*|lijinfeng|1
```
> * 报警订阅内容分成了四个信息，分别表示如下
     > * 名称，对于监控来说，名称就是node管理中的cluster名称
     > * 分组，对于上一节显示的监控配置，分组对应的是cpu，disk,意思是把不同的监控进行了分类，方便不同的人订阅自己关系的内容
     > * 订阅人， 后续章节（报警接入）中会说明这个报警人的具体信息是怎么配置的
     > * 订阅的级别

## 关于订阅级别

```
root@feng-pc:~# cat /opt/mydan/dan/.config |grep notify -A 6
notify:
  level:
    1: [ 'email' ]
    2: [ 'sms' ]
    3: [ 'sms', 'email' ]
  code: $ROOT/notify/code
```
> * 在这个配置文件中进行配置，这里显示的意思为，1级发送邮件，2级发送短信，3级发送邮件和短信

## 订阅的添加和取消
```
root@feng-pc:/opt/mydan/dan/subscribe/bin# ./subscribe -?
Usage:
     select [--name|--attr|--user|--level]
     $0
     $0 --name name1
     $0 --user user1
     $0 --name name1 --user user1
     insert
     $0 --add --name name1 --attr attr1 --user user1 --level 1
     delete [--name|--attr|--user|--level]
     $0
     $0 --del --name name1
     $0 --del --user user1
     $0 --del --name name1 --user user1
```
> * 根据帮助操作即可

## 查看打到订阅系统的消息
```
root@feng-pc:/opt/mydan/dan/subscribe/bin# ./show
```
> * 到这里为止，只有监控系统往订阅系统打消息
> * 可以把发布系统的stuck消息也打到订阅系统，/opt/mydan/dan/bootstrap/bin# ./control  -start watch2subscribe
