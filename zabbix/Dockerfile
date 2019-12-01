# Use existing docker image as a base
FROM ubuntu:latest

# ARG DEBIAN_FRONTEND=noninteractive
# https://askubuntu.com/a/1013396

# Installing zabbix
RUN apt update
RUN apt install wget -y
RUN wget https://repo.zabbix.com/zabbix/4.2/ubuntu/pool/main/z/zabbix-release/zabbix-release_4.2-1+bionic_all.deb
RUN dpkg -i zabbix-release_4.2-1+bionic_all.deb
# RUN apt update
RUN apt install zabbix-server-mysql zabbix-frontend-php -y
RUN apt install zabbix-agent -y

RUN mkdir /var/run/zabbix
RUN touch /var/run/zabbix/zabbix_server.pid
RUN chown -R zabbix:zabbix /var/run/zabbix

COPY zabbix_server.conf /etc/zabbix/zabbix_server.conf

# https://stackoverflow.com/a/32179054/11103492
ENTRYPOINT /usr/sbin/zabbix_server && tail -f /var/log/zabbix/zabbix_server.log
