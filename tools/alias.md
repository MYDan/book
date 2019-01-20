# mydan alias
```
root@feng-pc:~# mydan alias
alias ssh='/usr/bin/ssh'
```
> * mydan内部使用的alias, 比如mssh会用到ssh命令，但是ssh可能是别的程序或者说需要其他的参数，就可以通过别名来处理

## 例
```
root@feng-pc:~# mydan alias
alias ssh='/usr/bin/ssh'
root@feng-pc:~# mydan alias ssh=/bin/ssh
root@feng-pc:~# mydan alias
alias ssh='/bin/ssh'
```