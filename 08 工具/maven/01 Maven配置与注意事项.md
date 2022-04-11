# Windows下配置
1. 需要安装JDK
echo %JAVA_HOME%
echo %PATH%
2. 需要安装Maven
echo %M2_HOME%
echo  %PATH%
3. 更新maven
修改 M2_HOME为新路径即可

# MacOS下配置
1. 需要安装JDK
echo $JAVA_HOME
echo $PATH
2. 需要安装Maven
echo $M2_HOME
echo $PATH
3. 更新maven
创建新的链接：
ln -s apache-maven-3.3.6 apach-maven
设置M2_HOME指向链接并新增Path路径：
export M2_HOME=/home/bin/apache-maven
export $ PATH:$M2_HOME/bin
最好将上面的命令添加的shell脚本中，linux为~/.bashrc
升级maven：
不用像windows一样还要更改M2_HOME路径
新建新的链接指向新版本目录就好
ln -s apache-maven-3.3.9 apach-maven

# 关于~/.m2
1. mvn help:system
当执行这个命令时，初次会下载mavn-help-plugin
文件夹中存在pom文件和jar文件，被下载到本地仓库中，即~/.m2

# proxies

