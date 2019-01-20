# mydan range

> * range表达式，是一个操作对象描述的一种方式，支持多种格式的表达

## 范围
```
root@feng-pc:~# mydan range 'mydan-{1,2,6~9}' -l
mydan-6
mydan-1
mydan-9
mydan-8
mydan-7
mydan-2
```

## 获取集群机器
```
root@feng-pc:~# mydan range '{==project1==*??==*}'
127.0.0.1,localhost
```

> * 获取node机器管理中的操作对象，node中的数据分层了四层，第一层是cluster，第二层是属性，比如机房，模块， 第三层是操作对象，比如机器，第四层是编号或者状态，建议第四层用来做状态，这样监控系统可以屏蔽报警或者发布系统可以不发布屏蔽掉故障的的机器
> * mydan range '{??==*==*==*}'获取集群列表

## 通过插件获取列表

### 通过list插件获取列表
```
mydan range '{%%list==a}' #获取当前目录下a.list 文件中的列表
mydan range '{%%list==a,b}' #获取a.list 和b.list的机器列表
mydan range '{%%list}' ,获取所有以 .list文件为后缀的机器列表
```
> * 要读取的".list"后缀的文件要在当前的操作路径下才能读取
> * 所有的".list"文件必须不能有格式错误，否则会让range加载失败，因为range会把当前目录下所有".list"文件都加载进来

### 通过node插件获取列表
```
mydan range '{%%node}' #获取机器管理中全部机器
```

## 表达式

### 加法
```
mydan range 'mydan-test-{1~3},foo-{10~20},localhost'
```
> * 用逗号分隔，把操作对象叠加在一起

### 减法
```
mydan range 'mydan-test-{1~3},-localhost'
```
> * 用减号去掉不需要的对象

### 叠加
```
root@feng-pc:~# mydan range 'AA-{1~2}-{1~2}'  -l
AA-2-1
AA-1-2
AA-2-2
AA-1-1
```

### 过滤出
```
root@feng-pc:~# mydan range 'AA-{1~20},&/2/' -l
AA-20
AA-2
AA-12
```
> * 过滤出符合条件的列表

### 过滤掉
```
root@feng-pc:~# mydan range 'AA-{1~20},^/2/'
AA-{1,3~11,13~19}
```
> * 过滤掉符合条件的列表
