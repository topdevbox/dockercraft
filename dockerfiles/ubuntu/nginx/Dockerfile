FROM topdevbox/ubuntu-base
MAINTAINER Daniel <daniel@topdevbox.com>

RUN apt-get update && \
	apt-get upgrade -y && \
	apt-get autoclean && \
	apt-get autoremove && \
    apt-get clean

RUN apt-get install -y nginx