# mydan diagnosis
```
mydan diagnosis
```
> * 系统诊断工具

## 例
```
root@feng-pc:~# mydan diagnosis
os: Linux arch:x86_64
===========================================================================
disk/space/data
===========================================================================
disk/space/inode
===========================================================================
net/connect/tcp
---
ESTABLISHED: 21
LISTEN: 26
TIME_WAIT: 5
===========================================================================
net/ping/baidu
PING www.baidu.com (180.149.132.151) 56(84) bytes of data.
64 bytes from 180.149.132.151: icmp_seq=1 ttl=48 time=2.82 ms
64 bytes from 180.149.132.151: icmp_seq=2 ttl=48 time=3.20 ms
64 bytes from 180.149.132.151: icmp_seq=3 ttl=48 time=2.86 ms
--- www.baidu.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 2.823/2.962/3.203/0.181 ms
score: 100
```