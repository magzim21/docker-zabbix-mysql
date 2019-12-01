# docker-zabbix-mysql

Забиксу нужен sql сервер для работы. Зачастую они устанавливаются в одном месте. 
С точки зрения контейнеризации, лучше максимально разделять сервисы. Поэтому, я посчитал оптимальным сделать два контейнера: zabbix и mysql.

Процесс установки zabbix хорошо описан тут (https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-zabbix-to-securely-monitor-remote-servers-on-ubuntu-18-04 )

Для сервиса базы данных mysql я взял готовый контейнер. Особенности его использования( https://github.com/docker-library/docs/tree/master/mysql )

Все фиксы установки прокомментированы в докерфайлах. 
Было странно, что zabbix-server-mysql не создает /usr/share/doc/zabbix-server-mysql/create.sql.gz в контейнере. Этот дамп нужен для содания первоначальных таблиц в базе данных заббикса. Чтобы разобраться, я проделал такие-же шаги установки на полноценной Ubuntu aws instance - там этот дамп был в нужном месте (я его выкачал и воспользовался положив в mysql контейнер в /docker-entrypoint-initdb.d (https://github.com/docker-library/docs/tree/master/mysql#initializing-a-fresh-instance ).

Я настроил github & TravisCI, переменные окружения(для логинов). 
По коммиту images сбилденные в TravisCI  должны улетать на докерхаб.



Чтобы проверить как контейнеры работают вместе, нужно стянуть репозиторий и выполнить эту команду:
docker-compose -f zabbix-compose.yml up -d
Судя по stOut, zabbix server подключается к mysql и уже после появляются какие-то ошибки c zabbix agent. Пожалуйста, намекните где я ошибся.
Чтобы проверить как настроен travis ci, нужно сделать любой комит в orign master - через две минуты появится свежий контейрер на dockerhub.


Мне пригодились:
- .travis.yml вадидатор https://config.travis-ci.com/explore
- docker документация https://docs.docker.com/engine/reference/commandline/docker/
- zabbix документация https://www.zabbix.com/documentation/3.0/manual/concepts/server
- В процессе составил полезную команду для очистки докера docker rm --force $(docker container ls -qa); docker rmi --force $(docker images -q); (поместил в алиас)

