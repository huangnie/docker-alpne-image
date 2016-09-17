FROM alpine

ENV DEBIAN_FRONTEND huangnie

RUN apk update   

RUN apk add  mysql mysql-client 

# 添加文件夹下的 MYSQL 配置文件
ADD my.cnf /etc/mysql/my.cnf 

# 添加 MYSQL 的脚本
RUN mkdir /script
ADD create_db.sh /script/create_db.sh
ADD import_sql.sh /script/import_sql.sh
ADD run.sh /script/run.sh
RUN chmod 755 /script/*.sh  && chmod u+x /script/*.sh 

# 设置环境变量，用户名以及秘密
ENV MYSQL_USER admin
ENV MYSQL_PASS **Random**

# 设置主从复制模式下的环境变量
ENV REPLICATION_MASTER **False**
ENV REPLICATION_SLAVE **False**
ENV REPLICATION_USER replcate
ENV REPLICATION_PASS replcate

ENV MYSQL_USER root
ENV MYSQL_PASS root

WORKDIR /var/lib/mysql  

# 设置可以允许挂载的卷，可以用来备份数据库和配置文件
VOLUME  /var/lib/mysql 

# 设置可以映射的端口 
EXPOSE 3306
CMD sh /script/run.sh