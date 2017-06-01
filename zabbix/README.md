# Zabbix讲解
## 基本简介 [15min]
[Zabbix](http://www.zabbix.com/)是一个开源的企业级系统监控解决方案，系统结构见图1.
![图1](http://img1.51cto.com/attachment/201208/130335905.png)
- Zabbix Server：接收Agent上报的数据，写入数据库（- MySQL、Oracle等），支持linux，不支持windows；和Agent双向通信，支持向agent发送指令的方式
- Web Server: Zabbix Server端前端页面,用以展示监测数据和配置zabbix，用PHP实现，一般部署在Apache上，与OS平台无关
- Zabbix Agent：被监控主机需要安装agent程序来采集数据，网络设备通过SNMP方式采集数据

## 亲身体验 [20min]
[内网演示地址](https://www.zabbix.org/zabbix/index.php)

[在线演示](https://www.zabbix.org/zabbix/index.php)

[功能截图](http://www.zabbix.com/screenshots)

## 安装步骤 [10min]
### [Server](https://www.zabbix.com/documentation/3.2/manual/installation/install_from_packages/server_installation_with_mysql)
1. #### 配置源
    Zabbix在CentOS基本源里不可获得，因此必须配置EPEL 和Zabbix 官方repository

    * 安装EPEL repository
    ```
    yum install epel-release
    ```

    * 配置ZabbixZone package repository and GPG key
    ```
    rpm --import http://repo.zabbix.com/RPM-GPG-KEY-ZABBIX

    rpm -Uv http://repo.zabbix.com/zabbix/3.2/rhel/7/x86_64/zabbix-release-3.2-1.el7.noarch.rpms
    ```

1. #### 安装Zabbix server
    ```
    yum install zabbix-server-mysql zabbix-web-mysql zabbix-java-gateway
    ```

1. #### 修改zabbix-server配置
    配置文件在/etc/zabbix/zabbix_server.conf，
    修改以下参数：
    ```
    DBName=zabbix
    DBUser=root
    DBPassword=egova
    DBHost= <zabbx-db-server-host>
    ```   
    或者通过下面命令修改配置
    ```
    sed -i '/# DBName=/a\DBName=zabbix' /etc/zabbix/zabbix_server.conf
    sed -i '/# DBUser=/a\DBUser=root' /etc/zabbix/zabbix_server.conf
    sed -i '/# DBPassword=/a\DBPassword=egova' /etc/zabbix/zabbix_server.conf
    sed -i '/# DBHost=/a\DBHost=192.168.101.14' /etc/zabbix/zabbix_server.conf
    ```

1. #### 启动Server

    启动zabbix-server、httpd,并设置zabbix-server开机自动启动
    ```
    systemctl start zabbix-server
    systemctl restart httpd
    systemctl enable zabbix-server
    ```

1. #### 更换字体以处理图表中文乱码问题

    下载[字体文件](http://note.youdao.com/groupshare/?token=3A8B07484C6D4499A81DE8D70A9430C5&gid=48867582)，并存放在zabbix server的`/usr/share/zabbix/fonts/`目录

### [Agent](https://www.zabbix.com/documentation/3.2/manual/installation/install_from_packages/agent_installation)
#### CentOS安装步骤
1. ##### 安装zabbix-agent
    CentOS7
    ```
    groupadd zabbix
    useradd -g zabbix zabbix
    rpm -ivh http://repo.zabbix.com/zabbix/3.2/rhel/7/x86_64/zabbix-release-3.2-1.el7.noarch.rpm
    yum install -y zabbix-agent
    ```

    CentOS6
    ```
    rpm -ivh http://repo.zabbix.com/zabbix/3.2/rhel/6/x86_64/zabbix-release-3.2-1.el6.noarch.rpm
    yum install -y zabbix-agent
    ```


1. ##### 修改zabbix-agent配置

    vi /etc/zabbix/zabbix_agentd.conf

    Server=<zabbix-server-ip>
    ServerActive=<zabbix-server-ip>
    Hostname=<host-name>

    附修改配置命令，注意替换相应IP：
    ```
    sed -i 's/Server=127.0.0.1/Server=<SERVER-IP>/g' /etc/zabbix/zabbix_agentd.conf
    sed -i 's/ServerActive=127.0.0.1/ServerActive=<SERVER-IP>/g' /etc/zabbix/zabbix_agentd.conf
    sed -i 's/Hostname=Zabbix\sserver/Hostname=<AGENT-IP>/g' /etc/zabbix/zabbix_agentd.conf
    ```

1. ##### 启动zabbix-agent
    CentOS7
    ```
    systemctl start zabbix-agent
    ```
    CentOS6
    ```
    /etc/init.d/zabbix-agent start
    ```

#### Windows安装步骤

1. ##### 下载zabbix-agent安装包
    [下载地址](http://www.zabbix.com/downloads/3.2.0/zabbix_agents_3.2.0.win.zip)
2. ##### 安装zabbix-agent

    解压zabbix_agents_3.2.0.win.zip，将conf/zabbix_agentd.win.conf拷贝到C盘根目录，并重命名为zabbix_agentd.conf,并依次修改如下配置：
    ```
    Server=<zabbix-server-ip>
    ServerActive=<zabbix-server-ip>
    Hostname=<host-name>
    ```
    用管理员身份打开命令行窗口，切换到对应的zabbix_agentd.exe目录（根据操作系统版本自行选择win32或者win64）,通过下面命令启动：
    ```
    zabbix_agentd.exe --install
    zabbix_agentd.exe --start
    ```

## 安装常见问题 [5min]
1. Zabbix Server不支持window，建议使用centos 7.
1.

## 使用场景介绍
### 场景一：主机内存不足时发送短信给xxx用户 [5min]

### 场景二：数据库连接数超过400时，发送短信给xxx用户 [15min]
