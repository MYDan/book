# dashboard

## 安装
```
cd /opt/mydan/ && \
git clone https://github.com/MYDan/dashboard.git && \
/opt/mydan/perl/bin/perl Makefile.PL && \
make && make install
```

## 配置
```
[root@feng-pc ~]# cat /opt/mydan/dashboard/config.yml
appname: "dashboard"
layout: "main"
charset: "UTF-8"
template: "template_toolkit"
engines:
  template_toolkit:
    start_tag: '[%'
    end_tag:   '%]'
ssocallback: 'http://sso.mydan.org:8080/?ref='
ssologout: 'http://sso.mydan.org:8080/logout'
cookiekey: 'sid'
```

> * ssocallback: 未登录情况下跳转的sso地址
> * ssologout: sso登出链接
> * cookiekey: sso写的cookie的key名

## 启动
```
cp /opt/mydan/dashboard/bin/dashboard.web.5555 /opt/mydan/dan/bootstrap/exec/
```

# 普通用户登录

> * 用户通过web登录后，把自己的公钥匙在页面上保存
> * 在用户机器上安装mydan
> * 修改api指向dashboard地址，运行命令：mydan config api.addr=http://127.0.0.1:5555
> * 修改mydan角色，运行命令：mydan config agent.role=client
> * linux中的用户名和sso中的用户名不一致,可以添加环境变量 MYDan_username 指明sso中的名字。 export MYDan_username=foo

# 管理员权限管理
```
[root@feng-pc ~]# /opt/mydan/dashboard/tools/access  -?
Usage:
     $0 [--user username] [--add work||--del root] [--access 10.10.1.1]
```

> * 用上面命令给用户分配权限
> * 可以通过修改/opt/mydan/dashboard/code/access插件对接公司的权限系统

# sso 相关

> * 修改/opt/mydan/dashboard/code/sso 插件进行sso对接