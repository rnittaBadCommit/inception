FROM debian:buster

RUN	set -ex; \
	apk update && apk upgrade;

RUN	apk add mariadb mariadb-client;

RUN	mysql -e "CREATE DATABASE wpdb;"; \
		mysql -e "GRANT ALL ON wpdb. * TO 'wordpress'@'localhost' IDENTIFIED BY 'wordpress' WITH GRANT OPTION;";

VOLUME [ "./volume" ]

CMD ["mysqld"]
