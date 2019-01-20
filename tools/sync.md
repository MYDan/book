# mydan sync
```
root@feng-pc:~# mydan sync
sync: util.proxy,go,node.cache,pass,gateway,hosts
sync util.proxy ...
--2018-12-15 17:05:07--  http://127.0.0.1:5555/download/sync/util.proxy
正在连接 127.0.0.1:5555... 失败：拒绝连接。
sync util.proxy fail.
```
> * 从dashboard中同步配置到本地
> * 默认情况下 /opt/mydan/dan/.config 中配置的api地址是http://127.0.0.1:5555 ，如果dashboar不是在这个地址，需要对应的修改

## 修改api地址
```
root@feng-pc:~# mydan config api.addr=http://mydan.xxx.org:5555
```
> * 其中mydan.xxx.org是dashboard的地址

## 例
```
root@feng-pc:~# mydan sync
sync: pass,go,hosts,gateway,node.cache,util.proxy
sync pass ...
--2018-12-23 10:22:48--  http://mydan.xxx.org:5555/download/sync/pass
正在解析主机 mydan.xxx.org (mydan.xxx.org)... 10.10.10.11
正在连接 mydan.xxx.org (mydan.xxx.org)|10.10.10.11|:5555... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度： 234 [application/data]
正在保存至: “/opt/mydan/etc/util/conf/pass.tmp”
/opt/mydan/etc/util/conf/pass.tmp               100%[=======================================================================================================>]     234  --.-KB/s    in 0s
2018-12-23 10:22:49 (29.1 MB/s) - 已保存 “/opt/mydan/etc/util/conf/pass.tmp” [234/234])
sync go ...
--2018-12-23 10:22:49--  http://mydan.xxx.org:5555/download/sync/go
正在解析主机 mydan.xxx.org (mydan.xxx.org)... 10.10.10.11
正在连接 mydan.xxx.org (mydan.xxx.org)|10.10.10.11|:5555... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度： 1020 [application/data]
正在保存至: “/opt/mydan/etc/util/conf/go.tmp”
/opt/mydan/etc/util/conf/go.tmp                 100%[=======================================================================================================>]    1020  --.-KB/s    in 0s
2018-12-23 10:22:49 (145 MB/s) - 已保存 “/opt/mydan/etc/util/conf/go.tmp” [1020/1020])
sync hosts ...
--2018-12-23 10:22:53--  http://mydan.xxx.org:5555/download/sync/hosts
正在解析主机 mydan.xxx.org (mydan.xxx.org)... 10.10.10.11
正在连接 mydan.xxx.org (mydan.xxx.org)|10.10.10.11|:5555... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度： 475632 (464K) [application/data]
正在保存至: “/opt/mydan/etc/hosts.tmp”
/opt/mydan/etc/hosts.tmp                        100%[=======================================================================================================>] 464.48K   595KB/s    in 0.8s
2018-12-23 10:22:54 (595 KB/s) - 已保存 “/opt/mydan/etc/hosts.tmp” [475632/475632])
sync gateway ...
--2018-12-23 10:22:54--  http://mydan.xxx.org:5555/download/sync/gateway
正在解析主机 mydan.xxx.org (mydan.xxx.org)... 10.10.10.11
正在连接 mydan.xxx.org (mydan.xxx.org)|10.10.10.11|:5555... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度： 309 [application/data]
正在保存至: “/opt/mydan/etc/util/conf/gateway.tmp”
/opt/mydan/etc/util/conf/gateway.tmp            100%[=======================================================================================================>]     309  --.-KB/s    in 0s
2018-12-23 10:22:54 (20.9 MB/s) - 已保存 “/opt/mydan/etc/util/conf/gateway.tmp” [309/309])
sync node.cache ...
--2018-12-23 10:22:54--  http://mydan.xxx.org:5555/download/sync/node.cache
正在解析主机 mydan.xxx.org (mydan.xxx.org)... 10.10.10.11
正在连接 mydan.xxx.org (mydan.xxx.org)|10.10.10.11|:5555... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度： 1376256 (1.3M) [x-chemical/x-cache]
正在保存至: “/opt/mydan/etc/node/cache/current.tmp”
/opt/mydan/etc/node/cache/current.tmp           100%[=======================================================================================================>]   1.31M   591KB/s    in 2.3s
2018-12-23 10:22:56 (591 KB/s) - 已保存 “/opt/mydan/etc/node/cache/current.tmp” [1376256/1376256])
sync util.proxy ...
--2018-12-23 10:22:57--  http://mydan.xxx.org:5555/download/sync/util.proxy
正在解析主机 mydan.xxx.org (mydan.xxx.org)... 10.10.10.11
正在连接 mydan.xxx.org (mydan.xxx.org)|10.10.10.11|:5555... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度： 1271 (1.2K) [application/data]
正在保存至: “/opt/mydan/etc/util/conf/proxy.tmp”
/opt/mydan/etc/util/conf/proxy.tmp              100%[=======================================================================================================>]   1.24K  --.-KB/s    in 0s
2018-12-23 10:22:57 (173 MB/s) - 已保存 “/opt/mydan/etc/util/conf/proxy.tmp” [1271/1271])
```