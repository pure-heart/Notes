#
# MAINTAINER        Nick,Y.Peng <nickyp@dockerstu.com>
# DOCKER-VERSION    1.6.2
#
# Dockerizing CentOS7: Dockerfile for building CentOS images
#

# 构建Docker镜像必须要有一个基础镜像，即父镜像(可从官网pull也可自己制作)
FROM       centos:centos7.1.1503
# 指定维护者信息
MAINTAINER Nick,Y.Peng <nickyp@dockerstu.com>

# 设置时区环境变量（ENV环境变量在Dockerfile中可以写多个）
# 这些指定的环境变量，后续可以被RUN指令使用，容器运行起来之后，也可以在容器中获取这些环境变量
ENV TZ "Asia/Shanghai"
ENV TERM xterm

# ADD：添加/拷贝文件到container里面，还有一个拷贝命令是COPY
# 两者的区别如下：
# 前者比后者多两个功能；
#     1. 可直接将url对应的文件直接复制到container里面；
#     2. 如果复制的是tar压缩包文件，用ADD拷贝结束后会自动帮我们解压；
ADD aliyun-mirror.repo /etc/yum.repos.d/CentOS-Base.repo
ADD aliyun-epel.repo /etc/yum.repos.d/epel.repo

# RUN 后面是要执行的命令，每执行一条指令就是一层，所以Dockerfile采用的是分层的技术
RUN yum install -y curl wget tar bzip2 unzip vim-enhanced passwd sudo yum-utils hostname net-tools rsync man && \
    yum install -y gcc gcc-c++ git make automake cmake patch logrotate python-devel libpng-devel libjpeg-devel && \
    yum install -y --enablerepo=epel pwgen python-pip && \
    yum clean all

RUN pip install supervisor  # 安装进程管理工具
ADD supervisord.conf /etc/supervisord.conf  # 添加进程管理工具的主配置文件到指定目录下，一般是/etc目录

RUN mkdir -p /etc/supervisor.conf.d && \    # 为进程管理工具新建一个目录，用来存放启动其他服务的配置文件
    mkdir -p /var/log/supervisor            # 新建进程管理日志目录

EXPOSE 22   # Docker服务器开放的端口，供容器外部连接使用(在启动容器时做端口映射)

# 如果有多条ENTRYPOINT语句，那么只有最后一条生效
# ENTRYPOINT指的是container每次启动的时候需要执行的命令
ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf"]
