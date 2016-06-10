FROM topdevbox/mysql-base
MAINTAINER Daniel <daniel@topdevbox.com>
# How-To
# Local Build: docker build -t my/mysql:test .
# Local Run: docker run -i -t -v ~/mysql:/var/lib/mysql --name="mysql-run" my/mysql:test /bin/bash
# Deamon Run: docker run -v ~/mysql:/var/lib/mysql -d --name="mysql" -e "MYSQL_ROOT_PASSWORD=password" -p 3306:3306 my/mysql:test 

RUN rm -rf /var/lib/mysql && mkdir -p /var/lib/mysql /var/run/mysqld \
  && chown -R mysql:mysql /var/lib/mysql /var/run/mysqld \
  && chmod 777 /var/run/mysqld

RUN sed -i -e"s/^bind-address\s*=\s*127.0.0.1/bind-address = 0.0.0.0\n/" /etc/mysql/mysql.conf.d/mysqld.cnf

VOLUME /var/lib/mysql

ADD mysqld.64M-Memory.cnf /tmp/mysqld.64M-Memory.cnf
ADD mysqld.512M-Memory.cnf /tmp/mysqld.512M-Memory.cnf
ADD mysqld.2G-Memory.cnf /tmp/mysqld.2G-Memory.cnf
ADD mysqld.4G-Memory.cnf /tmp/mysqld.4G-Memory.cnf

RUN cp /tmp/mysqld.2G-Memory.cnf /etc/mysql/conf.d/mysqld.2G-Memory.cnf

ADD bootstrap.sh /bootstrap.sh
RUN chmod 755 /*.sh
ENTRYPOINT ["/bootstrap.sh"]

EXPOSE 3306

CMD ["mysqld"]