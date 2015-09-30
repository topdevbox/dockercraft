FROM topdevbox/base
MAINTAINER Daniel <daniel@topdevbox.com>

#percona database with tokudb plugin
#percona 5.6 server database with tokudb plugin

RUN apt-get update && \
	apt-get upgrade -y && \
	apt-get autoclean && \
	apt-get autoremove && \
    apt-get clean

RUN apt-key adv --keyserver keys.gnupg.net --recv-keys 1C4CBDCDCD2EFD2A

RUN echo "deb http://repo.percona.com/apt "$(lsb_release -sc)" main" | sudo tee /etc/apt/sources.list.d/percona.list

RUN echo "deb-src http://repo.percona.com/apt "$(lsb_release -sc)" main" | sudo tee -a /etc/apt/sources.list.d/percona.list

RUN apt-get update

RUN echo "percona-server-server-5.6 percona-server-server/root_password_again password dbpassword" | debconf-set-selections
RUN echo "percona-server-server-5.6 percona-server-server/root_password password dbpassword" | debconf-set-selections
RUN apt-get install -y percona-server-server-5.6 percona-server-client-5.6 percona-server-common-5.6 

RUN sed -i -- "s/bind-address/#bind-address/g" /etc/mysql/my.cnf

#RUN service mysql restart
#RUN mysql -u root -p"dbpassword" -e "GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'dbpassword' WITH GRANT OPTION;"
#RUN mysql -u root -p"dbpassword" -e "FLUSH PRIVILEGES;"


#RUN echo never > /sys/kernel/mm/transparent_hugepage/enabled
#RUN echo never > /sys/kernel/mm/transparent_hugepage/defrag

RUN apt-get install -y libjemalloc1 libjemalloc-dev
RUN sed -i -- "s/[mysqld_safe]/[mysqld_safe]\nmalloc-lib= /usr/include/jemalloc/g" /etc/mysql/my.cnf

RUN apt-get install -y percona-server-tokudb-5.6

RUN service mysql restart

RUN ps_tokudb_admin --enable -u root -p"dbpassword"

RUN service mysql restart


