# docker-zabbix-mysql

Забиксу нужен sql сервер для работы. Зачастую они устанавливаются в одном месте. 
С точки зрения контейнеризации, лучше максимально разделять сервисы. Поэтому, я посчитал оптимальным сделать два контейнера: zabbix и mysql
Все фиксы установки прокомментированы в докерфайлах.
Было странно, что zabbix-server-mysql   не создает /usr/share/doc/zabbix-server-mysql/create.sql.gz в контейнере. Этот дамп нужен для содания первоначальных таблиц в базе данных заббикса. Чтобы разобраться, я проделал такие-же шаги установки на полноценной Ubuntu aws instance - там этот дамп был в нужном месте (я его выкачал и воспользовался положив в свой отдельный mysql контейнер в /docker-entrypoint-initdb.d (https://github.com/docker-library/docs/tree/master/mysql#initializing-a-fresh-instance ).

Я настроил github & TravisCI, переменные окружения(для логинов). 
По коммиту images сбилденные в TravisCI  должны улетать на докерхаб.

Несмотря на все проделанные шаги, что-то не билдится. Пожалуйста, намекните где я ошибся. 