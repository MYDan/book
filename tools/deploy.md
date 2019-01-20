# mydan deploy
```
root@feng-pc:~# mydan deploy
SYNOPSIS
     $0 [--repo /my/repo ] [--link /my/link] [--version release-x.x.x]
        [--path /my/path ( default $repo/data ) ]
        [--keep 10 (default 10)]
        [--taropt '-m']
        Version 'release-x.x.x' and 'rollback:release-x.x.x' are the same
        Version backup refers to the $link.backup
        Version backup\d* refers to the $link.backup\d*
```
> * 本地发布切链接小工具

> * repo: 各版本的压缩包存放的路径
> * link: 应用的软链接
> * path: 包被解压后存放的路径，如果不指定，会放到repo/data路径下
> * keep: 保留的版本个数
> * taropt: 解压时添加的tar参数，默认已经添加-zxf,添加的参数紧接在tar命令之后，(如 --taropt "-m" 不要解压文件的修改时间)
> * 如果版本的名字规则是 backup\d* , 切换版本的操作变成了把link直接指向link.backup\d* ,切换版本的过程中，如果link是一个目录，会被从命名成 link.backup

> * rollback:release-x.x.x 如果版本是"rollback:"开头，会直接把"rollback:"这个前缀去掉

> * 如果A版本之前发布过并且解压包没有因为keep的限制被删除掉，这时候如果回滚回A版本，就不会重新从解压


## 例
```
root@feng-pc:/tmp# mydan deploy --repo /tmp/repo --link /tmp/apps --version 001
mkdir '/tmp/repo/data/001.1545719254.21590._tmp_explain'
tar -zxf '/tmp/repo/001' -C '/tmp/repo/data/001.1545719254.21590._tmp_explain'
rm -rf '/tmp/repo/data/001' && mv '/tmp/repo/data/001.1545719254.21590._tmp_explain' '/tmp/repo/data/001'
ln -fsn '/tmp/repo/data/001' '/tmp/apps'
root@feng-pc:/tmp# ll /tmp/apps
lrwxrwxrwx 1 root root 18 12月 23 14:27 /tmp/apps -> /tmp/repo/data/001/
root@feng-pc:/tmp# ll /tmp/repo
总用量 16
drwxr-xr-x  3 root root 4096 12月 23 14:27 ./
drwxrwxrwt 17 root root 4096 12月 23 14:27 ../
-rw-r--r--  1 root root  191 12月 23 14:27 001
drwxr-xr-x  3 root root 4096 12月 23 14:27 data/
```

> * /tmp/repo下是各个版本的程序包，每一个包是tar.gz文件，但是不需要文件后缀
