FROM php:5.6-fpm

RUN apt-get update
RUN apt-get install -y libfreetype6-dev
RUN apt-get install -y libjpeg62-turbo-dev
RUN apt-get install -y libmcrypt-dev
RUN apt-get install -y libpng12-dev

RUN docker-php-ext-install iconv mcrypt mysql
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd
RUN docker-php-ext-install zip
RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_mysql

RUN apt-get install -y wget

RUN wget http://wordpress.org/latest.tar.gz
RUN tar xzvf latest.tar.gz
RUN cp wordpress/wp-config-sample.php wordpress/wp-config.php
RUN rm -rf latest.tar.gz

COPY entrypoint /usr/local/bin/
RUN chmod +x /usr/local/bin/entrypoint

WORKDIR /var/www/html

EXPOSE 9000

ENTRYPOINT ["/usr/local/bin/entrypoint"]