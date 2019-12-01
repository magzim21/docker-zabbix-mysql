FROM mysql:latest
EXPOSE 3306/tcp
EXPOSE 33060/tcp
# ENV MYSQL_ALLOW_EMPTY_PASSWORD yes
ENV MYSQL_DATABASE zabbix
ENV MYSQL_USER zabbix-user
ENV MYSQL_PASSWORD zabbix-secure-password
ENV MYSQL_ROOT_PASSWORD root-secure-password
# WORKDIR /home
# COPY create_db.sql ./
# RUN mysql -u root < /home/create_db.sql
# CMD /bin/bash && sleep 100500 &
