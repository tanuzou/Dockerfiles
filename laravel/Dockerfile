#build stage
FROM amazonlinux
LABEL Name=laravel Version=0.0.1

# Timezone
RUN cp -f -p /usr/share/zoneinfo/Japan /etc/localtime

# install Package
RUN yum -y update && yum -y upgrade
RUN yum -y install httpd24 httpd24-tools gcc make git diffutils file 
RUN yum -y install php71 php71-devel 
RUN yum -y install php71-pdo php71-pecl-apcu php71-mysqlnd php71-opcache uuid-php71 vim which re2c php71-mbstring php71-php-pear php71-fpm

# Apache
RUN sed -i -e "s/Listen 80/Listen 8001/" /etc/httpd/conf/httpd.conf
RUN sed -i -e "s/AllowOverride None/AllowOverride All/" /etc/httpd/conf/httpd.conf
RUN sed -i -e "s/Options Indexes FollowSymLinks/Options -Indexes +FollowSymLinks/" /etc/httpd/conf/httpd.conf

# PHP
RUN echo 'date.timezone = Asia/Tokyo' >> /etc/php.ini

# PHP Composer
WORKDIR /tmp
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# Laravel 
WORKDIR /var
RUN mkdir /var/laravel && mkdir /var/laravel/www
RUN sed -i -e "s/\/var\/www\/html/\/var\/laravel\/www\/public/g" /etc/httpd/conf/httpd.conf

ENTRYPOINT /usr/sbin/httpd -D FOREGROUND
EXPOSE 8001
