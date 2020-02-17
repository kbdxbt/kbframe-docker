### 安装docker环境
- 这里准备的是一台刚重置的阿里云服务器，系统为：Linux Centos7.6。如果切换成其他虚拟机或者其他环境的可以查看官方文档进行安装<br/>https://docs.docker.com/install/linux/docker-ce/centos/
> 如已安装docker或者需要升级docker版本的，先停止docker服务 systemctl stop docker<br/>
- 卸载软件包
```
yum erase docker \
    docker-client \
    docker-client-latest \
    docker-common \
    docker-latest \
    docker-latest-logrotate \
    docker-logrotate \
    docker-selinux \
    docker-engine-selinux \
    docker-engine \
    docker-ce
```
- 删除相关配置文件： 
```
find /etc/systemd -name '*docker*' -exec rm -f {} \;
find /etc/systemd -name '*docker*' -exec rm -f {} \;
find /lib/systemd -name '*docker*' -exec rm -f {} \;
rm -rf /var/lib/docker
rm -rf /var/run/docker  
```
#### 安装dokcer
> 这里均采用root用户安装，省略sudo，不是root权限需加上sudo命令<br/>

1.软件包安装： 
```
yum install -y yum-utils device-mapper-persistent-data lvm2
```
2.添加yum源：
```
yum-config-manager \
--add-repo \
   https://download.docker.com/linux/centos/docker-ce.repo
```
3.安装最新版本： 
```
yum install docker-ce -y
```
4.启动并开机自启：
```
systemctl start docker
systemctl enable docker
```
5.查看docker版本： 
```
docker version
```
####安装docker-compose
> 以下以 Linux 为例
  更多详见官方文档：https://docs.docker.com/compose/install/
  
1.安装  
```
curl -L https://get.daocloud.io/docker/compose/releases/download/1.22.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
```
or
```
curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
2.赋予权限
```
chmod +x /usr/local/bin/docker-compose
```
3.查看版本号
```
docker-compose version
```
#### 镜像加速
国内从 Docker Hub 拉取镜像有时会遇到困难，此时可以配置镜像加速器。国内很多云服务商都提供了国内加速器服务，例如：

我们以 Azure 中国镜像 https://dockerhub.azk8s.cn 为例进行介绍。对Ubuntu 16.04+、Debian 8+、CentOS 7适用
1.编辑/etc/docker/daemon.json
```
touch /etc/docker/daemon.json
vi /etc/docker/daemon.json
```
2.填写内容
```
{
  "registry-mirrors": [
    "https://dockerhub.azk8s.cn",
    "https://reg-mirror.qiniu.com"
  ]
}
```
3.重新启动服务
```
systemctl daemon-reload
systemctl restart docker
```