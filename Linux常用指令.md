## Linux常用指令

#### 压缩

`tar -zcvf file.tar.gz file`

#### 解压

`tar -zxvf file.tar.gz`

#### Linux centos重启
　　1 `reboot`   普通重启
　　2 `shutdown -r now` 立刻重启(root用户使用)
　　3 `shutdown -r 10` 过10分钟自动重启(root用户使用)
　　4 `shutdown -r 20:35` 在时间为20:35时候重启(root用户使用)
　　如果是通过shutdown命令设置重启的话，可以用shutdown -c命令取消重启
　#### Linux centos关机
　　1 `halt` 立刻关机
　　2 `poweroff` 立刻关机
　　3 `shutdown -h now` 立刻关机(root用户使用)
　　4 `shutdown -h 10` 10分钟后自动关机
　　如果是通过shutdown命令设置关机的话，可以用shutdown -c命令取消重启

#### 手动安装JDK

1 下载上传jdk安装包

2 解压安装包

3 配置环境变量

`vim /etc/profile`文件内加上如下内容

`#java environment
export JAVA_HOME=/usr/jdk1.8.0_211
export CLASSPATH=.:${JAVA_HOME}/jre/lib/rt.jar:${JAVA_HOME}/lib/dt.jar:${JAVA_HOME}/lib/tools.jar
export PATH=$PATH:${JAVA_HOME}/bin\`

`source /etc/profile`让配置文件生效

