### 在window平台下使用手册

#### 简介
```
window下需要借助cygwin，Cygwin是一个在windows平台上运行的类UNIX模拟环境。
对于mydan来说使用方式和linux下基本一样，主要需要说明的是Cygwin的安装、包依赖，服务依赖。
```

#### 安装Cygwin
```
到Cygwin官网https://www.cygwin.com 下载最新的setup.exe程序。下载后双击打开
1. 选择安装方式：Install from Internet 
2. 选择安装的路径，如: C:\cygwin-mydan 
3. 选择本地包路径，这个路径是安装过程中存放的下载包的路径，使用默认的即可，随意 
4. 选择你的网络链接，看情况而定，默认是不需要代理的Direct Connection 
5. 选择下载网点，这里需要选择一个可用的下载网点，推荐ftp://ftp.mirrorsservice.org 
6. 选择需要安装的包： 
     在View中选Full，然后搜索下面的包，并且勾选上 
         curl: Multi-protocol file transfer tool 
         wget: Utility to retrieve files from the WWW via HTTP and FTP 
         make: The GNU version of the `make` utility 
         rsync: Fast remote file transfer program (can use existing data to minimize transfer) 
         cygrunsrv: NT/W2K service initiator 
         cron: Vixie's cron 
7. 点击下一步，完成安装.
```
#### 启动相关服务
```
mydan需要crontab服务来启动，所以需要把crontab服务做开机启动。（当然也可以开启启动的时候直接启动mydan的bootstrap）
操作步骤如下：
1. 找到安装目录下的批处理文件Cygwin（bat文件，如安装在C:\cygwin-mydan，则这个文件的全路径名应该是C:\cygwin-mydan\Cygwin.bat), 右键选择“以管理员身份运行”。正常情况下会打开一个和linux中的shell类似的控制台 
2. 一般服务器的Administrator肯定设有密码的，所以这个时候要配置cron服务并以验证密码以管理员权限登陆才能启动cron，大家按照下面的提示操作：
     $ cron-config 
     Do you want to install the cron daemon as a service? (yes/no) yes 
     Enter the value of CYGWIN for the daemon: [ ] crontab 
     Do you want the cron daemon to run as yourself? (yes/no) yes 
     Please enter the password for user 'Administrator':键入密码 
     Reenter:再次键入密码 
3. 启动 cygserver: cygrunsrv -I cygserver -p /usr/sbin/cygserver -e "CYGWIN=server" 
4. 将cron安装为windows服务: cygrunsrv -I crontab -p /usr/sbin/cron.exe 
5. 启动cron服务： cygrunsrv -S crontab 
6. 用cronevents 查看运行日志,如出现 “can't switch user context” 错误用命令：passwd -R 来设置密码 
```

#### 安装mydan
```
和在linux上一样，在控制台中运行安装命令 curl -L install.mydan.org|bash 

点击查看已有的编译好的perl,如果列表中没有合适您系统版本的编译好的perl，安装脚本会使用系统的perl，这样可能会话很长的时间，同时安装依赖模块的时候可能失败，如果您在新的系统版本中使用了mydan，欢迎上传您编译好的perl
```

#### Cygwin参考资料
```
https://www.cygwin.com 
http://blog.chinaunix.net/uid-10540984-id-1629742.html 
https://www.cnblogs.com/Li-Cheng/articles/4397208.html 
https://www.cnblogs.com/yougewe/archive/2015/12/03/5016409.html 
```


