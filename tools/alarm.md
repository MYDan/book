# mydan alarm
```
mydan alarm 
#alarm number-of-seconds command ..
```
> * 设置超时闹钟运行命令
> * 到超时时间后会给运行的进程发送KILL（9）信号
## 例
```
root@feng-pc:~# mydan alarm 3 echo ok
ok
```