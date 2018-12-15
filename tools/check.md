# mydan check
```
root@feng-pc:~# mydan check
SYNOPSIS
     $0 proc.num
          proc.num name    [=~]foo [<>=]5 ...
          proc.num cmdline  =foo   '>1' '<4'
          proc.num exe      ~foo   '>1'
          proc.time name =foo '>180'
        http.check
          http.check [get|post] http://127.0.0.1/stat code 200 300
          http.check [get|post] http://127.0.0.1/stat grep ok health
        net.port.listen
          net.port.listen tcp 80 22
          net.port.listen udp 53
          --debug
```
> * 检查服务的小工具