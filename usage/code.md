# 仓库管理 (gitlab&svn)

在一些情况下，可能需要代码仓库管理员管理多套git和svn。如果需要查询某个用户的权限项目和项目的归属人，或者停用某个用户，操作比较麻烦，仓库管理模块可以解决一些代码仓库管理的问题。

对git的管理是通过直接调用api。对于svn是通过修改管理机上的文件，然后提交到代码仓库，svn服务器定时同步最新，或者直接从管理机同步到svn服务器。

```
root@feng:# mydan code
nofind config file:/opt/mydan/dan/code/config
root@feng:# cp /opt/mydan/dan/code/config.example  /opt/mydan/dan/code/config
root@feng-pc:/opt/mydan/dan/code# mydan code
---
- apiurl: http://gitlab.mydan.org/api/v4
  name: git1
  token: xxxxxxxxxxxxxxxx
- apiurl: https://gitlab.mydan.com/api/v4
  name: git2
  token: xxxxxxxxxxxxxxxx
- name: svn1
  path:
  - /opt/mydan/dan/code/temp/svn1/*/*.txt
SYNOPSIS
     $0 [--search user]
     $0 [--list]
     $0 [--block user]
     $0 [--unblock user]

     $0 [--name name]
```
## 解释

### 配置
> * 不写任何参数的情况下，会打印出配置文件的信息和参数帮助
> * 配置文件是一个yaml格式的文件，是一个数组，每个元素代表一个git或者svn，如果存在apiurl则表示是git，否则是svn
> * token就是git中的private_token
> * name 是给每个仓库起名，可以起一样的名字，在通过mydan code 操作时可以通过--name来指定只操作某个仓库
> * svn类型的配置文件中的path，使用匹配文件路径的方式和linux命令中的ls一样

### 参数
> * search: 搜索用户，一般是邮箱，比如lijinfeng2011@gmail.com,git可以通过用户名和邮箱搜索，svn只可以通过邮箱来搜索
> * list: 列出所有的用户，如果checkuser插件私有化定制了，会把仓库里面的处于active状态的用户查一遍用户状态（是否离职）
> * block: 停用用户。对于svn来说，就是把svn对应的所有配置文件中该用户上加前缀 block__ , 重新启用时把前缀去掉
> * unblock：启用用户

## 例

### 搜索用户
```
root@feng:# mydan code --search lijinfeng2011@gmail.com 

[1]: lijinfeng2011@gmail.com git group         http://gitlab.mydan.org/groups/mg1    lijinfeng2011@gmail.com
[1]: lijinfeng2011@gmail.com git project.group http://gitlab.mydan.org/g2t/proj1     @ByGroup
[2]: lijinfeng2011@gmail.com git project.group http://gitlab.mydan.org/g5g/Proj      mydan1@gmail.com @GroupOwner
[3]: lijinfeng2011@gmail.com git project.group http://gitlab.mydan.org/g5g/Pa     mydan2@gmail.com @GroupOwner
[4]: lijinfeng2011@gmail.com git project.user  http://gitlab.mydan.org/lijinfeng2011/test_2  @Self
[5]: lijinfeng2011@gmail.com git project.user  http://gitlab.mydan.org/lijinfeng/test    lijinfeng@gmail.com @ProjectOwner
[6]: lijinfeng2011@gmail.com git project.user  http://gitlab.mydan.org/user1/mm1         NoFind
[7]: lijinfeng2011@gmail.com git project.group http://gitlab.mydan.org/grouptest1/mx1    @ByGroup
[1]: lijinfeng2011@gmail.com svn group   /opt/mydan/dan/code/temp/svn1/p1/AccessConfig.txt [groups] MYDan_G_T_1_rw
[2]: lijinfeng2011@gmail.com svn project /opt/mydan/dan/code/temp/svn1/p1/AccessConfig.txt [/mydan/code/test] lijinfeng2011@gmail.com = rw
[3]: MYDan_G_T_1_rw  svn bygroup /opt/mydan/dan/code/temp/svn1/p1/AccessConfig.txt [/my/dan] @MYDan_G_T_1_rw = rw
```
#### git中的项目归属通过以下顺序查找
> * @ByGroup 表示这个用户在这个组里面，以组权限为准
> * @GroupOwner 用户不在这个项目组里面，如果这个项目是属于某个组的，找这个组的owner
> * @Self 这个项目就是这个用户自己的
> * @ProjectOwner 找这个项目的owner
> * NoFind 什么都没有匹配上

### 获取用户列表
```
root@feng:# mydan code --list
[1]: git mydan1@gmail.com active
[2]: git mydan2@gmail.com block
[3]: git mydan3@gmail.com active
[4]: git mydan4@gmail.com active
[1]: svn mydan1@gmail.com active
```

### 停用用户
```
root@feng:# mydan code --block lijinfeng2011@gmail.com
git lock user.email=lijinfeng2011@gmail.com user.id=123
```

### 启用用户
```
root@feng:# mydan code --unblock lijinfeng2011@gmail.com
git unlock user.email=lijinfeng2011@gmail.com user.id=123
```

### 指定仓库执行
```
root@feng:# mydan code --name svn --search lijinfeng2011@gmail.com 

[1]: lijinfeng2011@gmail.com svn group   /opt/mydan/dan/code/temp/svn1/p1/AccessConfig.txt [groups] MYDan_G_T_1_rw
[2]: lijinfeng2011@gmail.com svn project /opt/mydan/dan/code/temp/svn1/p1/AccessConfig.txt [/mydan/code/test] lijinfeng2011@gmail.com = rw
[3]: MYDan_G_T_1_rw  svn bygroup /opt/mydan/dan/code/temp/svn1/p1/AccessConfig.txt [/my/dan] @MYDan_G_T_1_rw = rw
```

> * 仓库名可以重名

### 其他

查看：[checkuser](/tools/checkuser.md)

> * 需要实现自己的插件/opt/mydan/dan/code/plugin/checkuser.private
> * 如果没有定义自己的插件则跳过
