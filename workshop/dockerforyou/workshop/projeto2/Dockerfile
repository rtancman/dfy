FROM php:5.6-fpm


RUN wget http://wordpress.org/latest.tar.gz
RUN tar xzvf latest.tar.gz
RUN cp ~/wordpress/wp-config-sample.php ~/wordpress/wp-config.php
RUN rsync -avP ~/wordpress/ /var/www/html/