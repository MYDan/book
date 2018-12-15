# 报警接入

## 配置
```
root@feng-pc:~# cat /opt/mydan/dan/.config |grep ^notify -A 5
notify:
  level:
    1: [ 'email' ]
    2: [ 'sms' ]
    3: [ 'sms', 'email' ]
  code: $ROOT/notify/code
```
> * 从报警的接入来看，当前分了3个级别，第一级发邮件，第二级发短信，第三极发邮件和短信。
> * 平台是不认识也不识别短信还是邮件，email和sms这两个字符串对应的code下的插件名

## 编写邮件和短信插件
```
root@feng-pc:/opt/mydan/dan/notify/code# ls  /opt/mydan/dan/notify/code
email  email.private  sms
```
> * email、sms如果需要发邮件和短信，就需要重新实现它
> * 重写的插件，在mydan从新升级的时候可能会把您自己写的插件给覆盖了，为了避免这种问题，mydan中多个地方都可以通过添加 ".private"后缀的方式来解决，比如email的插件名写成email.private，系统判断到有这个文件，就读取这个私有的插件，这样mydan更新是，就不会覆盖用户的插件。

### 配置人员信息
```
root@feng-pc:~# cat /opt/mydan/etc/util/conf/contact.private
lijinfeng:
  email: lijinfeng2011@gmail.com
  sms: 133xxxxxxxx
```
> * 这里的email和sms，需要和插件名称对上

```
root@feng-pc:～# cat /opt/mydan/etc/util/conf/team.private
t1: [ 'user1', 'user2' ]
t2: [ 'user3', 'user4' ]
```
> * 组里一般是人的列表，也可以是另一个组，也可以是对应到上一个章节中的值班表

## 关于 值班人、组、人的关系理解
> * 订阅系统可以给 值班人、组、人做订阅
> *  name:level格式表示值班人, @teamname表示一个组，其他字符表示人
> * 值班表中可以写组，例如某个排班的某个级别是一个组的信息
> * 组中也可以是值班人，例如组A中包含 foo:1 和 bar:1,表示该组成员是当前foo排班表里面的第一值班人和bar值班表里面的第一值班人
> * 这样就会有一个问题，如果组和值班人相互引用，会导致死循环，这里的解决逻辑是，只会往下找五层，如果解析出来的列表有不是人的格式，这部分直接被去掉
