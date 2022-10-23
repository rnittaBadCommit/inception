FROM debian:buster

RUN	set -ex; \
	apk update && apk upgrade;

RUN set -ex; \
	apk add mysql mysql-client \
	php7-phar php7-fpm php7-common php7-session php7-iconv php7-json php7-gd php7-curl php7-xml php7-mysqli php7-imap php7-cgi fcgi php7-pdo php7-pdo_mysql php7-soap php7-xmlrpc php7-posix php7-mcrypt php7-gettext php7-ldap php7-ctype php7-dom \
	wget unzip;

COPY	./srcs/php.ini /etc/php/7.3/fpm/php.ini

# create db
RUN	service php7.3-fpm start; \
		service mysql start && mysql -u root; \
		mysql -e "CREATE DATABASE wpdb;"; \
		mysql -e "GRANT ALL ON wpdb. * TO 'wordpress'@'localhost' IDENTIFIED BY 'wordpress' WITH GRANT OPTION;";

# install phpmyadmin
RUN	set -eux; \
		wget https://files.phpmyadmin.net/phpMyAdmin/5.0.2/phpMyAdmin-5.0.2-all-languages.tar.gz; \
		tar -xvf phpMyAdmin-5.0.2-all-languages.tar.gz; \
		rm phpMyAdmin-5.0.2-all-languages.tar.gz; \
		mv phpMyAdmin-5.0.2-all-languages phpmyadmin; \
		mv phpmyadmin/ /var/www/html/

# install wordpress
RUN	wget https://wordpress.org/latest.tar.gz; \
		tar -xvzf latest.tar.gz; \
		rm latest.tar.gz; \
		mv wordpress /var/www/html/

COPY	./srcs/wp-config.php ./var/www/html/wordpress/

RUN chown -R www-data:www-data /var/www/html/wordpress;

CMD service php7.3-fpm stop && service php7.3-fpm start; \
	service mysql start; \
	tail -f /dev/null;
