# mydan git
```
root@feng-pc:~# mydan git
Usage:
  git -i ssh-key-file git-command
  git -u foo git-command
```
> * git工具，和默认的git一样，git中的默认工具不能指定ssh-key文件路径和用户，这个就是为了解决能制定key文件的问题
> * 比如当前是在root用户下进行操作，需要操作feng的仓库，需要指定-u feng 指明使用的是feng这个用户的key

## 例

### 指定key
```
root@feng-pc:/tmp/xx# mydan git -i /home/feng/.ssh/id_rsa clone https://github.com/MYDan/mayi
正克隆到 'mayi'...
remote: Enumerating objects: 390, done.
remote: Counting objects: 100% (390/390), done.
remote: Compressing objects: 100% (264/264), done.
remote: Total 4140 (delta 192), reused 283 (delta 116), pack-reused 3750
接收对象中: 100% (4140/4140), 632.70 KiB | 193.00 KiB/s, 完成.
处理 delta 中: 100% (2378/2378), 完成.
检查连接... 完成。
```
### 指定用户
```
root@feng-pc:/tmp/xx# mydan git -u feng clone https://github.com/MYDan/mayi
正克隆到 'mayi'...
remote: Enumerating objects: 390, done.
remote: Counting objects: 100% (390/390), done.
remote: Compressing objects: 100% (264/264), done.
remote: Total 4140 (delta 192), reused 283 (delta 116), pack-reused 3750
接收对象中: 100% (4140/4140), 632.70 KiB | 603.00 KiB/s, 完成.
处理 delta 中: 100% (2378/2378), 完成.
检查连接... 完成。
```