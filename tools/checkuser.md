# mydan checkuser
请查看之前[仓库管理](/usage/code.md)章节

## 查看用户状态

```
root@feng:# mydan checkuser --email lijinfeng
active
```
> * 这是仓库管理中用到的插件，用于判断用户是处于什么状态，比如是否离职。
> * 仓库管理需要把已离职人员的git和svn账号给block掉。

## 插件

> * 您需要实现自己的插件 /opt/mydan/dan/code/plugin/checkuser.private
> * 默认调用/opt/mydan/dan/code/plugin/checkuser插件，返回active状态。
