# Centos7离线安装Zabbix
下载解压[zabbix.zip](https://pan.baidu.com/s/1bo2xK1T)并进入解压后目录依次执行：
## 安装Server
```
install-mysql.sh
install-zbserver.sh
install-zbweb.sh
```
## 安装agent
`rpm -ivh agent/zabbix-agent-3.2.6-1.el7.x86_64.rpm`

## 离线安装说明
离线安装是利用`yum install --downloadonly`的downloadonly选项可以下载所有相关依赖包的功能来是现实的。步骤如下：
1. 准备一台联网主机（虚拟机），使用`yum install --downloadonly`（例如`yum install --downloadonly --downloaddir=/home/vagrant/rpms/mysql mysql-server`）命令下载好依赖包
2. 准备一台没有网络的主机（虚拟机），将之前下载下的包全部拷贝到该主机上，然后通过`rpm -ivh package-a.rpm package-b.rpm ...`离线安装
