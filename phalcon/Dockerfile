#build stage
FROM amazonlinux
LABEL Name=phalcon Version=0.0.1

# Timezone
RUN cp -f -p /usr/share/zoneinfo/Japan /etc/localtime

# install Package
RUN yum -y update && yum -y upgrade
RUN yum -y install httpd24 httpd24-tools gcc make git diffutils file 
RUN yum -y install php71 php71-devel 
RUN yum -y install php71-pdo php71-pecl-apcu php71-mysqlnd php71-opcache uuid-php71 vim which re2c php71-mbstring php71-php-pear php71-fpm

# Apache
RUN sed -i -e "s/Listen 80/Listen 8000/" /etc/httpd/conf/httpd.conf
RUN sed -i -e "s/AllowOverride None/AllowOverride All/" /etc/httpd/conf/httpd.conf
RUN sed -i -e "s/Options Indexes FollowSymLinks/Options -Indexes +FollowSymLinks/" /etc/httpd/conf/httpd.conf

# PHP
RUN echo 'date.timezone = Asia/Tokyo' >> /etc/php.ini

# PHP Composer
WORKDIR /tmp
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# Phalcon
WORKDIR /tmp
RUN git clone git://github.com/phalcon/cphalcon.git && cd cphalcon/build && ./install
RUN echo 'extension=phalcon.so' > /etc/php.d/phalcon.ini

# Phalcon-tools
WORKDIR /usr/local/share
RUN git clone git://github.com/phalcon/phalcon-devtools.git && cd phalcon-devtools && ./phalcon.sh
RUN ln -s /usr/local/share/phalcon-devtools/phalcon.php /usr/bin/phalcon

ENTRYPOINT /usr/sbin/httpd -D FOREGROUND
EXPOSE 8000
