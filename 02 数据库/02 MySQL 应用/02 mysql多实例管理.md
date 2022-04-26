# 部署多个mysql实例
基于一个mysql应用，初始化三次，生成三个独立的数据目录。
也就是生成三个独立的实例。

mysql 安装方式：
- 二进制安装
- 源代码安装
- rpm等系统安装工具

这次用二进制的方式安装mysql应用：

```shell
[root@oahc mysql]# 
[root@oahc mysql]# cd ~/download/
[root@oahc download]# 
[root@oahc download]# 
[root@oahc download]# pwd
/root/download
[root@oahc download]# 
[root@oahc download]# wget https://mirrors.sohu.com/mysql/MySQL-5.6/mysql-5.6.49-linux-glibc2.12-x86_64.tar.gz
```

