# 应用操作

## 路径

> * 应用操作配置目录:/opt/mydan/etc/project/apps/
> * 应用检查配置目录:/opt/mydan/etc/project/check/
> * 应用发布配置目录:/opt/mydan/etc/project/deploy/

## 应用操作
### 配置
```
[root@feng-pc]# ls /opt/mydan/etc/project/apps/project1/
start  stop
[root@feng-pc]# cat /opt/mydan/etc/project/apps/project1/start
#!/bin/bash
echo start
```
### 操作
```
[root@feng-pc]# mydan rcall  -r 127.0.0.1 apps project1 start
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
start [1]: [#!/bin/bash
echo start
]
start
====================================================================
```

## 应用检查

### 配置
```
[root@feng-pc]# ls /opt/mydan/etc/project/check/
project1  project2
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
### 操作
```
[root@feng-pc]# mydan rcall  -r 127.0.0.1 check project1
run .. 100% 1/1
############################## RESULT ##############################
====================================================================
127.0.0.1[1]:
http://127.0.0.1:5555 <> mydan :OK
tcp => 127.0.0.1:8080 :OK
done.
====================================================================
```

## 应用发布
### 配置
```
[root@feng-pc]# ls /opt/mydan/etc/project/deploy/
project1  project2
[root@feng-pc]# cat /opt/mydan/etc/project/deploy/project1
link: /data/apps/project1
path: /data/package/project1
```

### 程序包
```
[root@feng-pc]# ls /opt/mydan/etc/dashboard/download/package/
project1
[root@feng-pc]# ls /opt/mydan/etc/dashboard/download/package/project1/
v0.1  v0.1.md5  v0.2  v0.2.md5
```
### 启动dashboard

> * [dashboard](/access/dashboard.md)

### 修改api地址

> * 把要发布程序的机器把api指到对应的dashboar: mydan config api.addr=http://127.0.0.1:5555

### 操作
```
[root@feng-pc]# mydan rcall  -r 127.0.0.1 deploy project1 deploy 
```

# 其他

> * 以上三个功能对应发布管理中的 m.apps,m.check,m.deploy
