# 部署多个mysql实例
基于一个mysql应用，初始化三次，生成三个独立的数据目录，则可以实现多实例安装。

这次用二进制的方式安装MySQL应用：

```shell
[root@oahc mysql]# cd ~/download/
[root@oahc download]# pwd
/root/download
[root@oahc download]# wget https://cdn.mysql.com//Downloads/MySQL-8.0/mysql-8.0.28-linux-glibc2.12-x86_64.tar.xz
[root@oahc download]# mkdir -p ~/Applications/mysql/{3306,3307}
[root@oahc download]# tree ~/Applications/mysql/
[root@oahc download]# tar -Jxvf mysql-8.0.28-linux-glibc2.12-x86_64.tar.xz 
[root@oahc download]# ls -l
[root@oahc download]# cp mysql-8.0.28-linux-glibc2.12-x86_64 ~/Applications/mysql/main
[root@oahc download]# vim ~/Applications/mysql/3306/my.cnf


```

配置文件(3306)：

```properties
[client]

[mysqld]
port=3306
socket=/root/Applications/mysql/3306/mysql.sock
basedir=/root/Applications/mysql/main
datadir=/root/Applications/mysql/3306/data
log-bin=/root/Applications/mysql/3306/mysql-bin
server-id=1

[mysqld_safe]
log-error=/root/Applications/mysql/3306/mysql_3306_error.log
pid-file=/root/Applications/mysql/3306/mysqld_3306.pid
```

启停脚本(3306)：

```shell
port=3306
mysql_user="root"
Cmdpath="/root/Applications/mysql/main/bin"
mysql_sock="/root/Applications/mysql/${port}/mysql.sock"
mysqld_pid_file_path="/root/Applications/mysql/${port}/mysqld_${port}.pid"

start(){
    if[! -e "$mysql_sock"];then
        printf “Start MySQL...\n”
        /bin/sh ${Cmdpath}/mysqld_safe --defaults-file=/root/Applications/mysql/${port}/my.cnf --pid-file=${mysqld_pid_file_path} 2>&1 > /dev/null & 
        sleep 3
    else
        printf "MySQL is running...\n"
        exit 1
    fi
}

stop(){
if[! -e "$mysql_sock"];then
	printf “MySQL is Stopped...\n”
	exit 1


}
```

