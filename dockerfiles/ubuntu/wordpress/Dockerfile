FROM php:7-apache
MAINTAINER Daniel <daniel@topdevbox.com>
# How-To
# Local Build: docker build -t my/wp:test .
# Local Run: docker run -i -t --name wpcli -v ~/wp-content:/var/www/html/wp-content -v ~/wp-config.php:/var/www/html/wp-config.php my/wp:test /bin/bash
# Deamon Run: docker run -d --name wp -p 80:80 -v ~/wp-content:/var/www/html/wp-content -v ~/wp-config.php:/var/www/html/wp-config.php my/wp:test

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libbz2-dev \
        libcurl4-gnutls-dev \
        wget \
        unzip \
    && docker-php-ext-install -j$(nproc) iconv mcrypt zip pdo_mysql mysqli mcrypt ftp curl hash bz2 \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && cd /tmp/ \
    && wget https://wordpress.org/wordpress-4.5.2.zip \
    && unzip wordpress-4.5.2.zip \
    && rm -Rrf /var/www/html \
    && mv ./wordpress /var/www/html \
    && apt-get remove -y wget unzip \
    && apt-get autoremove -y \
	&& apt-get clean autoclean \
    && rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && rm -rfR /var/www/html/wp-content


VOLUME /var/www/html/wp-content
VOLUME /var/www/html/wp-config.php

EXPOSE 80
CMD ["apache2-foreground"]