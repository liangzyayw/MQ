# Centos7 image
# VERSION 7.8.2003
# Author: RTC

# 指定基于的容器镜像
FROM daduber/centos7.8.2003

# 维护者信息
MAINTAINER lzy

# 指定RTC环境安装路径
ADD  zookeeper.tar.gz  /usr/local/
ADD  jdk.tar.gz /usr/local/

# 设置时间与安装依赖
RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
  && echo 'Asia/Shanghai' >/etc/timezone  \
  && mkdir /usr/local/zookeeper/data  \
  && mkdir /usr/local/zookeeper/logs

# 设置环境变量
ENV JAVA_HOME=/usr/local/jdk
ENV PATH=${JAVA_HOME}/bin:$PATH
ENV LC_ALL=en_US.UTF-8

#设置挂载点
VOLUME ["/usr/local/zookeeper/data","/usr/local/zookeeper/logs"]

#设置端口
EXPOSE  2181

# 容器启动时执行指令
ENTRYPOINT [ "/bin/sh","/usr/local/zookeeper/bin/zookeeper.sh"]
