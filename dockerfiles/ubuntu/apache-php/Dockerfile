FROM php:7-apache
MAINTAINER Daniel <daniel@topdevbox.com>
# How-To
# Local Build: docker build -t my/php7:test .
# Local Run: docker run -i -t --name php my/php7:test /bin/bash
# Deamon Run: docker run -d --name php -p 80:80 -v ~/html:/var/www/html my/php7:test

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libbz2-dev \
        libcurl4-gnutls-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt zip pdo_mysql mysqli mcrypt ftp curl hash bz2 \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && apt-get autoremove -y \
	&& apt-get clean autoclean \
    && rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

VOLUME /var/www/html

EXPOSE 80
CMD ["apache2-foreground"]