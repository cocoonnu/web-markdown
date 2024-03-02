# 第一章 Linux 学习笔记

首先是在 mac 上配置开发环境，初始需要 VMware、Linux 系统镜像、Termius 三个组成部分。这里是先安装 CentOS 7 可以直接参考文档：https://juejin.cn/post/7216707319643471930，使用的是民间提供的 `CentOS-7-aarch64` 版本，此后 JDK 版本需要 arrch64。然后就是使用 Termius 进行 SSH 连接虚拟机：使用 `ip addr` 查看虚拟机地址和登录用户名密码就行直接连接上了，然后要保证虚拟机一直处于运行状态。

- linux 常用命令：https://juejin.cn/post/7070045539705815076

- vim 常用命令：https://juejin.cn/post/7070699702732783623



**配置静态 IP**

主要目的是保证系统 IP 地址为静态，首先打开虚拟机网络适配器设置为桥接模式 WIFI 模式。重启服务器发现 IP 地址已经改变了，因此 Termius 需要重新连接一下。然后打开文件 `vi /etc/sysconfig/network-scripts/ifcfg-ens160`，编辑完文件后还需要执行：`service network restart`。最后执行 `ip addr` 和 `ping www.baidu.com` IP 地址和检查网络

```
# 打开电脑的WIFI设置查看然后照样填入
IPADDR=192.168.10.123 # 我填的是当前服务器的ip地址
GATEWAY=192.168.10.1
NETMASK=255.255.255.0
DNS1=8.8.8.8
```



**配置 yum**

yum 是 Linux 系统的软件安装工具，需要设置一下镜像源和下载一些常用工具

```bash
yum install wget -y
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo_bak
wget http://mirrors.aliyun.com/repo/Centos-altarch-7.repo -O /etc/yum.repos.d/CentOS-Base.repo
yum makecache
yum install -y gcc automake autoconf libtool make vim net-tools
```



## 1.1 Linux 常用软件安装

### 1.1.1 JDk 安装教程

官网或者镜像源下载 JDK 安装包，必须下载对应好的 linux 版本

1. https://repo.huaweicloud.com/java/jdk/8u171-b11/
2. https://www.oracle.com/java/technologies/downloads/#java8



解压到 /usr/local 下：`tar -zxvf jdk-8u171-linux-x64.tar.gz -C /usr/local`

添加环境变量然后执行 `source /etc/profile` 再使用 `java -version` 查看是否安装成功

```
JAVA_HOME=/usr/local/jdk1.8.0_171
PATH=$JAVA_HOME/bin:$PATH
```



### 1.1.2 Nginx 安装教程

官网或者镜像源下载 Nginx 安装包：https://nginx.org/en/download.html

后面参考文档即可：https://cyborg2077.github.io/2022/10/18/ReggieOptimization/#Nginx

