# Linux网络相关概念
网络是多台计算机用某种介质连接起来就是网络。
信号是通过各种介质传递的信息。
1秒一个信号，持续施加电压8秒，那么对方就会理解为传递了8个信号。
传递信息之前规定多长时间为一个信号，就是协议。

# 内核空间和用户空间
linux系统分为2个层次：用户空间和内核空间。
所有用户进程都在用户空间运行，所有内核功能都在内核空间运行，网络功能就属于内核功能。
配置ip这类操作是在内核中生效的，只是用户通过工具在用户空间对ip地址进行配置管理。
配置IP的两种方式：
1. 命令配置（临时生效）：立即生效，不能永久生效
2. 配置文件（永久生效）：不会立即生效，永久生效。
内核在启动时会读取配置文件，内核启动后就不会再去读取配置文件，所以当内核启动后修改配置文件需要手动让内核重新读取配置文件。

# 网卡的命名规则
在centos6之前，网卡的命名是用序号进行的，比如eth0、eth1等。
新的 CentOS 7 开始对于网卡的编号有另一套规则，网卡的界面代号与网卡的来源有关,网卡名称会是这样分类的：
1. eno ：主板板载网卡，代表由主板 BIOS 内置的网卡，eno1、eno2等
2. ens ：热插拔网卡，代表由主板 BIOS 内置的 PCI-E 界面的网卡，USB、扩展槽之类的网卡，ens1、ens2等
3. enp ：代表 PCI-E 界面的独立网卡，可能有多个插孔，因此会有 s0, s1... 的编号~  enps1、enps2等
4. eth0 ：如果上述的名称都不适用，就回到原本的默认网卡编号
ens33为自动备援模式，名称定为ens33（桥接）。

# root用户登陆系统
linux默认有一个root用户，它是独一无二的。
生产机中不建议使用root用户登陆，因为root用户权限相当大。

# ifconfig命令
```shell
yum search  ifconfig
已加载插件：fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.cn99.com
 * extras: mirrors.163.com
 * updates: mirrors.163.com
============================================= 匹配：ifconfig ==============================================
net-tools.x86_64 : Basic networking tools

yum install net-tools.x86_64
已加载插件：fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.cn99.com
 * extras: mirrors.163.com
 * updates: mirrors.163.com
正在解决依赖关系
--> 正在检查事务
---> 软件包 net-tools.x86_64.0.2.0-0.25.20131004git.el7 将被 安装
--> 解决依赖关系完成

依赖关系解决

===========================================================================================================
 Package                架构                版本                                   源                 大小
===========================================================================================================
正在安装:
 net-tools              x86_64              2.0-0.25.20131004git.el7               base              306 k

事务概要
===========================================================================================================
安装  1 软件包

总下载量：306 k
安装大小：917 k
Is this ok [y/d/N]: y
Downloading packages:
警告：/var/cache/yum/x86_64/7/base/packages/net-tools-2.0-0.25.20131004git.el7.x86_64.rpm: 头V3 RSA/SHA256 Signature, 密钥 ID f4a80eb5: NOKEY
net-tools-2.0-0.25.20131004git.el7.x86_64.rpm 的公钥尚未安装
net-tools-2.0-0.25.20131004git.el7.x86_64.rpm                                       | 306 kB  00:00:00     
从 file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 检索密钥
导入 GPG key 0xF4A80EB5:
 用户ID     : "CentOS-7 Key (CentOS 7 Official Signing Key) <security@centos.org>"
 指纹       : 6341 ab27 53d7 8a78 a7c2 7bb1 24c6 a8a7 f4a8 0eb5
 软件包     : centos-release-7-6.1810.2.el7.centos.x86_64 (@anaconda)
 来自       : /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
是否继续？[y/N]：y
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  正在安装    : net-tools-2.0-0.25.20131004git.el7.x86_64                                              1/1 
  验证中      : net-tools-2.0-0.25.20131004git.el7.x86_64                                              1/1 

已安装:
  net-tools.x86_64 0:2.0-0.25.20131004git.el7                                                              

完毕！


ifconfig
ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.31.163  netmask 255.255.255.0  broadcast 192.168.31.255
        inet6 fe80::2adb:fa14:1631:2a66  prefixlen 64  scopeid 0x20<link>
        ether 00:0c:29:c7:ad:77  txqueuelen 1000  (Ethernet)
        RX packets 55266  bytes 28606686 (27.2 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 9204  bytes 622355 (607.7 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 96  bytes 8112 (7.9 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 96  bytes 8112 (7.9 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0


```

