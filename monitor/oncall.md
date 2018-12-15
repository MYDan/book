# 值班管理
> * 上一节讲的订阅系统，订阅人和报警接入有关，报警接入和值班系统有关系，这里先穿插讲一下值班系统，不需要轮班的可以跳过这一节。

## 路径
> * /opt/mydan/dan/oncall

## 编辑排版配置，一个班是一个配置文件
```
root@feng-pc:~# cat /opt/mydan/dan/oncall/conf/example
---
site: cn
pivot: 2017.06.10
queue:
 - user1
 - user2
 - user3
---
site: us
pivot: 2017.06.11 20:00
timezone: America/Los_Angeles
duration: '19:10 ~ 7:20'
period: 7
level: [ 1, 2 ]
day: [ 1, 2, 3, 4, 5 ]
queue:
 - usr1
 - usr2
 - usr3
```

## 生成排版
```
root@feng-pc:/opt/mydan/dan/oncall/bin# ./make example
```

## 查看排班
```
root@feng-pc:/opt/mydan/dan/oncall/bin# ./list example
 Thu 00:00
2018-12-15           user1           user3           user2
 Sun 00:00
2018-12-16           user2           user1           user3
 Mon 00:00
2018-12-17           user3           user2           user1
 Mon 11:10
2018-12-17            usr1            usr3
 Mon 23:21
2018-12-17           user3           user2
 Tue 00:00
2018-12-18           user1           user3           user2
 Tue 11:10
2018-12-18            usr1            usr3
 Tue 23:21
2018-12-18           user1           user3
 Wed 00:00
2018-12-19           user2           user1           user3
 Wed 11:10
2018-12-19            usr1            usr3
 Wed 23:21
2018-12-19           user2           user1
 Thu 00:00
2018-12-20           user3           user2           user1
 Thu 11:10
2018-12-20            usr1            usr3
 Thu 23:21
2018-12-20           user3           user2
 Fri 00:00
2018-12-21           user1           user3           user2
```
 
> *  排班配置好后可以直接在订阅系统和下一节的报警接入中使用，比如在订阅系统中给 example:1 这个用户订阅上报警，就会解析成example这个排班当前的第一值班人，找到值班人后再去找他对应的手机号码或者邮件地址