# 快速安装

## 安装mydan
```
 curl -L http://update.mydan.org|sudo bash
```
> * 在所有的机器上安装mydan，安装目录是/opt/mydan

## 启动mydan服务
```
/opt/mydan/dan/bootstrap/bin/bootstrap --install
```
> * mydan的agent启动端口为65111

## 生成一对密钥
```
cd /opt/mydan/etc/agent/auth && \
ssh-keygen -f mydan -P "" && \
mv mydan mydan.key && \
echo success
```
> * 在控制机上生成一对公钥私钥

## 拷贝公钥
```
scp /opt/mydan/etc/agent/auth/mydan.pub 10.10.10.3:/opt/mydan/etc/agent/auth/mydan.pub
```
> * 把公钥拷贝到所有的机器上


