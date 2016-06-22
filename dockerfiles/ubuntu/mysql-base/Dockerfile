FROM topdevbox/ubuntu-base
MAINTAINER Daniel <daniel@topdevbox.com>
# How-To
# Local Build: docker build -t my/mysql:test .
# Local Run: docker run -i -t my/mysql:test /bin/bash
# Deamon Run: docker run -d --name="mysql-run" -e "MYSQL_PASSWORD=password" -p 3306:3306 my/mysql:test

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get install -y mysql-server mysql-client \
    && apt-get autoremove -y \
	&& apt-get clean autoclean

#   && rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log \
#	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 3306
