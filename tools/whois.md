# mydan whois
```
root@feng-pc:~# mydan whois localhost
cluster:
project idc1    127.0.0.1       1
project1        idc1    127.0.0.1       1
project1        idc1    localhost       1
project1        idc2    127.0.0.1       1
hosts:
localhost       127.0.0.1
localhost.localdomain   127.0.0.1
localhost4      127.0.0.1
localhost4.localdomain4 127.0.0.1
test123.mydan.org       127.0.0.1
```

> * 查询某个资源在哪个集群中
> * mydan whois 和 mydan w 两个命令等同
> * 如果细心看，发现这个命令的输出包含两个信息，一个是cluster一个是host。cluster 就是机器管理中的内容，host是/opt/mydan/etc/hosts文件中记录的内容，这个文件和/etc/hosts 文件的格式一致，配置了这个文件，在mydan中可以直接使用里面的机器名来调用。如果一个机器有多个ip,多个机器名，可以用 n\d\*-hostname 来配置内网地址，用w\d\*-hostname 来配置外网地址，这种情况下用mydan whois查询任何一个ip或者机器名，命令会返回这个机器所有的信息
