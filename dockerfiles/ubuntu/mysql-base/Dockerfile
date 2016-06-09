FROM topdevbox/ubuntu-base
MAINTAINER Daniel <daniel@topdevbox.com>
# How-To
# Local Build: docker build -t my/mysql:test .
# Local Run: docker run -i -t my/mysql:test /bin/bash
# Deamon Run: docker run -d --name="mysql-run" -e "MYSQL_PASSWORD=password" -p 3306:3306 my/mysql:test


RUN apt-get update && \
	apt-get upgrade -y && \
	apt-get autoclean && \
	apt-get autoremove && \
    apt-get clean

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get install -y mysql-server \
    supervisor && apt-get clean
RUN apt-get install -y mysql-client \
		&& apt-get clean

RUN rm -rf /var/lib/apt/lists/*

RUN sed -i -e"s/^bind-address\s*=\s*127.0.0.1/bind-address = 0.0.0.0\n/" /etc/mysql/mysql.conf.d/mysqld.cnf

EXPOSE 3306
