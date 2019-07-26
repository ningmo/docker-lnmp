######
# See: https://hub.docker.com/_/php/
######

FROM php:5.6-fpm
MAINTAINER micooz <micooz@hotmail.com>

######
# You can install php extensions using docker-php-ext-install
######

RUN usermod -u 1000 www-data

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev
        # libpng12-dev
RUN docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd 


RUN pecl install -o -f redis \
	&&  rm -rf /tmp/pear \
	&&  docker-php-ext-enable redis

RUN docker-php-ext-install -j$(nproc)  mysqli  zip mbstring pdo_mysql 

RUN apt-get install wget autoconf -y
RUN apt-get update
### mq
#RUN wget https://github.com/alanxz/rabbitmq-c/releases/download/v0.5.0/rabbitmq-c-0.5.0.tar.gz 
#RUN tar -zxvf rabbitmq-c-0.5.0.tar.gz && \
#	cd rabbitmq-c-0.5.0/ && \
#	autoconf -i  && \
#	./configure --prefix=/usr/local/rabbitmq-c &&  \
#	make && make install

#RUN wget http://pecl.php.net/get/amqp-1.6.1.tgz && \
#	tar zxvf amqp-1.6.1.tgz && \
#	cd amqp-1.6.1 && \
#	phpize && \
#	./configure --with-php-config=/usr/local/bin/php-config --with-amqp --with-librabbitmq-dir=/usr/local/rabbitmq-c && \
#	make && make install && \
#	docker-php-ext-enable amqp

RUN docker-php-ext-install -j$(nproc)  bcmath 