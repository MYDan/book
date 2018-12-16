# mydan deploy
```
root@feng-pc:~# mydan deploy
SYNOPSIS
     $0 [--repo /my/repo ] [--link /my/link] [--version release-x.x.x]
        [--path /my/path ( default $repo/data ) ]
        [--keep 10 (default 10)]
        Version 'release-x.x.x' and 'rollback:release-x.x.x' are the same
        Version backup refers to the $link.backup
        Version backup\d* refers to the $link.backup\d*
```
> * 本地发布切链接小工具

> * repo: 各版本的压缩包存放的路径
> * link: 应用的软链接
> * path: 包被解压后存放的路径，如果不指定，会放到repo/data路径下
> * keep: 保留的版本个数

> * 如果版本的名字规则是 backup\d* , 切换版本的操作变成了把link直接指向link.backup\d* ,切换版本的过程中，如果link是一个目录，会被从命名成 link.backup

> * rollback:release-x.x.x 如果版本是"rollback:"开头，会直接把"rollback:"这个前缀去掉

> * 如果A版本之前发布过并且解压包没有因为keep的限制被删除掉，这时候如果回滚回A版本，就不会重新从解压
